---
aliases : Job System
---
# Overview
Separate data from function.
Multi-core processing 
Save multi-threading.

## Benefits
Average core count increasing, but most cores go unused.

### Multithreading problems : 
- Thread safe code is difficult to write.
- Race conditions (waiting for other threads...)
- Context switching is expensive

### Solution
- Job system manage this for you. 
- Allows to focus entirely on the game specific code. 

# Implementation
```CSharp

//Job definition
using Unity.Jobs;
using UnityEngine;
using UnityEngine.Jobs;

[ComputeJobOptimization]
public struct MovementJob : IJobParallelForTransfrom
{
	public float moveSpeed;
	public float topBOund;
	public float bottomBound;
	public float deltaTime;
	
	public void Execute(int index, TransformAccess transform)
	{
		Vector3 pos = transform.position;
		pos += moveSpeed * deltaTime * (transform.rotation * new Vector3(0,0,1);
		
		if(pos.z < bottomBound)
			pos.z = topBound;
		
		transform.position = pos;
	}
}


//GameManager
public class GameManager : MonoBehaviour
{

	//Variables...
	
	TransformAccessArray transforms;
	MovementJob moveJob;
	JobHandle moveHandle;
	
	void OnDisable()
	{
		moveHandle.Complete();
		transforms.Dispose();
	}
	
	void Start()
	{
		transforms = new TransformAccessArray(0,-1);
		AddShips(enemyShipCount);
	}
	
	void Update()
	{
		moveHandle.Complete();
		
		moveJob = new MovementJob()
		{
			moveSpeed = enemySpeed;
			topBound = topBound;
			bottomBound = bottomBound,
			deltaTime = Time.deltaTime;
		}
		moveHandle = moveJob.Schedule(transforms);
		JobHandle.ScheduleBatchedJobs();
	}
	
	void AddShips(int amount)
	{
		moveHandle.Complete();
		transforms.capacity = transforms.length + amount;
		
		//logic
		
		transforms.Add(obj.transform);
	}
	
}



```

Interfaces : 
IJob : standard job -> process something on a single.
IJobParallelFor : allow to iterate over a collection of items that need to be processed and spread them over multiple threads.
IJobParallelForTransform : specifies the above interfaces for moving / working with a transform.

