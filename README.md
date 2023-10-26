using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class SnakeController : MonoBehaviour
{
    public float moveSpeed  = 5;
    public float steerSpeed = 180;
    public int Gap;
    public int Score;
    public Text scoreText;
    public GameObject bodyPrefab;
    List<GameObject> BodyParts = new List<GameObject>();
    List<Vector3> PositionHistory = new List<Vector3>();
 

    // Update is called once per frame
    void Update()
    {
    {
        transform.position += transform.forward * moveSpeed * Time.deltaTime;

        float steerDirection = Input.GetAxis("Horizontal");

        transform.Rotate(Vector3.up * steerDirection * steerSpeed * Time.deltaTime);

       

 PositionHistory.Insert(0, transform.position);

        int index = 0;
        foreach (var body in BodyParts)
        {
            Vector3 point = PositionHistory[Mathf.Clamp(index * Gap, 0, PositionHistory.Count - 1)];

            Vector3 moveDirection = point - body.transform.position;
            body.transform.position += moveDirection * moveSpeed * Time.deltaTime;

            body.transform.LookAt(point);

            index++;
        }

        scoreText.text = Score.ToString(); 
    }





   
    }
    void GrowSnake()
    {
        GameObject body = Instantiate(bodyPrefab);
        BodyParts.Add(body);
    }
    private void OnTriggerEnter(Collider other)
    {
        if(other.gameObject.tag == "food")
       



 {
            GrowSnake();
            Destroy(other.gameObject);
            Score++;
        }
    }}







