## Definition 
A system contains behaviour (logic). (ex. Render system, health system). 
It is composed of :
- a filter : returns every [[Entity]] that has specific [[Component]].
- a job  : applies the job to the returned entities. 