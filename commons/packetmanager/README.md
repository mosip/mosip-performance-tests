This folder contains performance test scripts and test data of Packet manager module.

### Environment Required:-
***Below modules should be running in kubernetes setup***

* Kernel audit service
* Kernel authmanager service
* Packetmanager service

### Data prequisite:-
* Sample Reg ID's values are stored and can be updated based on the environment in the file ridPacketManager.txt.
* Sample document names are stored and can be updated based on the requirement in the file documentNames.txt.
* Sample field names are stored and can be updated based on the requirement in the file fieldNames.txt.
* Sample modality values are stored and can be updated based on the environment in the file modalityValues.txt.
* Sample field values are stored and can be updated based on the environment in the file searchFieldsRequestBody.csv.
* Sample tag values are stored and can be updated based on the environment in the file tags.txt.

### How to run JMeter scripts:-

* For the test execution part we have a Packet Manager Test Script which will do all the execution tasks.
* We need to take care of the prerequisites first for which we have one thread group Auth Token Generation (Setup) for the creation of authorization token which we will further use in our execution. 
* All the creation tasks which will happen that will automatically save the tokens created to a file in the bin folder of JMeter which will be used further by our test script for execution.
* In the test script we have 11 execution thread groups for all the scenario's, where the main test execution will take place.
* The Packetmanager module scenario's which we are considering here are - Get Documents, Validate Packet, Search Field, Search Fields, Get Biometrics, Get Audits, Get MetaInfo, Get Tags, Add Tags, Update Tags. Delete Tags and Create Packet.
* All the thread groups will run in a parallel manner & if we don't want to run all of them we can disable the one which we don't want to run.
* Also for viewing the results or output of our test we have added certain listener test elements at the end of our test script which are - View Results Tree, Endpoint Level Report, Scenario Level Report.
* We have a test element named 'User Defined Variables' in Test script where the server IP, server port, protocol, clientId, secretKey, appId, testDuration, rampUp, process and source all these are parameterized & can be changed based on our requirements which will further reflect in the entire script.



### Designing the workload model for performance test execution

* Calculation of number of users depending on Transactions per second (TPS) provided by client

* Applying little's law
	* Users = TPS * (SLA of transaction + think time + pacing)
	* TPS --> Transaction per second.

* For the realistic approach we can keep (Think time + Pacing) = 1 second for API testing
	* Calculating number of users for 10 TPS
		* Users= 10 X (SLA of transaction + 1)
		       = 10 X (1 + 1)
			   = 20


			   
### Usage of Constant Throughput timer to control Hits/sec from JMeter

* In order to control hits/ minute in JMeter, it is better to use Timer called Constant Throughput Timer.

* If we are performing load test with 10TPS as hits / sec in one thread group. Then we need to provide value hits / minute as in Constant Throughput Timer
	* Value = 10 X 60
			= 600

* Dropdown option in Constant Throughput Timer
	* Calculate Throughput based on as = All active threads in current thread group
		* If we are performing load test with 10TPS as hits / sec in one thread group. Then we need to provide value hits / minute as in Constant Throughput Timer
	 			Value = 10 X 60
					  = 600
		  
	* Calculate Throughput based on as = this thread
		* If we are performing scalability testing we need to calculate throughput for 10 TPS as 
          Value = (10 * 60 )/(Number of users)
		  
