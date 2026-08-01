AWS Lambda's max execution timeout is 900 seconds (15 minutes). Default is 3 seconds, 
configurable in 1-second increments up to 900. If a function hits the timeout, 
Lambda forcefully terminates it — mid-execution, no partial results saved.

For workloads that genuinely need longer than 15 minutes, the standard pattern is 
AWS Step Functions to orchestrate multiple Lambda invocations rather than trying to extend 
a single function's runtime.
