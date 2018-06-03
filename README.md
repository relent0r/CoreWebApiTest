# CoreWebApiTest
.net core gitlab ci build

pre-req : I have an nsx edge with a load balancer thats sending all port 80 traffic to the ingress controllers for external connectivity.

This is a test web api built to test gitlab CI using the docker executor

The .gitlab-ci.yml contains three stages
build-dotnet
build-docker
deploy

build-dotnet uses the microsoft dotnet latest container to run the publish command then will upload the resulting binaries to the gitlab server as artifacts

build-docker uses the docker:dind service to build the container using the aspnetcore:2.0 image. Then tag it and push it to the container registry

deploy uses the alpine container which downloads a version of kubectl based on a variable, creates the kube config using certificate authentication and then updates the manifest to generate unique pods, services, ingress. After this it then creates them in kubernetes.

TODO

complete the registry push(gotta get my ssl config sorted on the registry), remove testing commands, add logging during stages, add vCloud NSX Edge configuration script. Add a more secure way of getting client certificates for kube config and use namespace specific ones instead of a big bad global admin.
