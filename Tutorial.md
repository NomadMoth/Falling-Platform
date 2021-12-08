# Falling Platform Tutorial

## 1. Variables

Create one private Rigidbody variable, two public floats, a public GameObject and a public BoxCollider.

    Rigidbody rb;
    public float dropDelay = 1f;
    public float respawnDelay = 4f;
    public GameObject spawnPoint;
    public BoxCollider boxCollider;
    
In the Start function, use GetComponent to reference the Rigidbody of the platform.

void Start()
    {
        rb = GetComponent<Rigidbody>();
    }
  
## 2. Functions
  
Create two new functions, one to drop the platform and another to bring the platform back to the spawn point 
mentioned in the variables.
  
    void DropPlatform()
    {
        rb.isKinematic = false;
        boxCollider.enabled = false;
    }
  
    void SpawnPlatform()
    {
        rb.isKinematic = true;
        boxCollider.enabled = true;
        transform.position = spawnPoint.transform.position;
    }
  
## 3. Triggers
  
Create an OnTriggerEnter function as well as an OnTriggerExit function. These will be used to invoke the DropPlatform and SpawnPlatform functions.
  
    void OnTriggerEnter(Collider other)
    {
        if (other.tag == "Player")
        {
            Invoke("DropPlatform", dropDelay);
        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.tag == "Player")
        {
            Invoke("SpawnPlatform", respawnDelay);
        }
    }
  
Ensure that the player has the "Player" tag in the inspector within Unity to allow the script to work correctly.
  
## 4. In Unity
  
Create an empty game object, rename to "FallingPlatform". Create two child game objects, one empty game object
which will serve as the spawn point, and a cube to serve as the platform. Also add an new box collider to the
cube/platform, enlarge it to surround the cube/platform and set it as a trigger.
  
![Screenshot 2021-12-08 194119](https://user-images.githubusercontent.com/72862464/145273540-507c3fc1-d00a-4044-8d4f-51890e09659d.jpg)
  
Attach the script to the cube and assign the spawn point and box collider to the appropriate boxes in the
inspector.
  
![Screenshot 2021-12-08 194145](https://user-images.githubusercontent.com/72862464/145273655-f2d24482-9e7f-4301-91b2-66717a82b814.jpg)

Now run the game and jump onto the platform to ensure that it works.
