# Overview
Ecs works in opposition to the "classic" way of programming in Unity.
Monobeheviours / Data - Processing Coupled / Largely dependant on reference types.
This "Classic" way of working has several problems : 
- the data is scattered, it makes loading from memory to cache very slow.
- Unnecessary extra data is often provided.
- Processing is done one at the time. (single threaded).


It's a paradigm shift from Object Oriented Programming to Data Oriented design.
Splitting the games in three parts : 
- [[Entity]]
- [[Component]]
- [[System]]

Pure ECS Vs Hybrid ECS

**Example  :** 
```CSharp
public class Rotator : MonoBehaviour {

	public float speed;
	
}

class RotatorSystem : ComponentSystem {
	
	struct Components
	{
		public Rotator rotator;
		public Transform transform;
	}
	
	protected override void OnUpdate()
	{
		foreach (var e in GetEntities<Components>())
		{
			e.transform.Rotate(0f, e.rotator.speed * Time.deltaTime, 0f);
		}
	}
}

```

# Benefits
- Extremely performant code 
- Easier to write higly optimized code;
- Easier to write reusable code.
- Gives a leverage on modern hardware architectre
- [[ Archetypes]] are tightly packed in memory
- Use the [[Burst Compiler]].
- Use the [[CSharp Job System]]

The [[CSharp Job System|Job System]] and ECS are not the same thing, but they work well together and are often seen used at the same time.

# Implementation
Component example : 
```CSharp
	[Serializable]
	public struct MoveSpeed : IComponentData
	{
		public float Value;
	}
	
	public class MoveSpeedComponent : ComponentDataWrapper<MoveSpeed> { }
```
The wrapper allows to put the component on an object in the Unity Editor.

System Example : 
```CSharp
public class MovementSystem : JobComponentSystem
{
	[ComputeJobOptimization]
	struct MovementJob : IJobProcessComponentData<Position, Rotation, MoveSpeed>
	{
		public float topBound;
		public float bottomBound;
		public float deltaTime;

		public void Execute(ref Position position, [ReadOnly] ref Rotation rotation, [ReadOnly] ref MoveSpeed moveSpeed)
		{
			//Logic
		}	
	}
	
	protected override JobHandle OnUpdate(JobHandle inputDeps)
	{
	
		MovementJob moveJob = new MovementJob
		{
			//init variable.
		}
		JobHandle moveHandle = moveJob.Schedule(this, 64, inputDeps);
		
		return moveHandle;
	}


}
```
