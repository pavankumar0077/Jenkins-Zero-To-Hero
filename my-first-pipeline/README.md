# A simple jenkins pipeline to verify if the docker agent configuration is working as expected.

1) Here in the pipeline JENKINNS requested DOCKER TO CREATE ONE CONTAINER (IT USES DOCKER PIPELINE PULGIN THAT WE CONFIGURED)
2) It(Pipeline plugin) talk to the DOCKER AND said can you give me one container so that i will execute my pipeline that is node js related application
3) Docker gave the node js container, AS SOON AS IT EXECUTE THE CONTAINER WILL STOPPED
4) No running conatiner at all, WHEN THERE IS REQUEST THEN THE CONTAINER WILL BE CREATED.

