# CoreWebApiTest
.net core gitlab ci build

pre-req - I have an nsx edge with a load balancer thats sending all port 80 traffic to the ingress controllers for external connectivity.
        - I have an nginx ingress controller in its own namespace which provides ingress to pods.
        - I have a httpd instance running with the ca.crt located on it for the docker.dind service.

This is a test web api built to test gitlab CI using the docker executor. Probably the biggest challenge was getting it all to work with non public ca and dns zone. 

The .gitlab-ci.yml contains three stages
build-dotnet
build-docker
deploy

build-dotnet uses the microsoft dotnet latest container to run the publish command then will upload the resulting binaries to the gitlab server as artifacts

build-docker uses the docker:dind service to build the container using the aspnetcore:2.0 image. Then tag it and pushes it to the container registry.
Note : The registry is using an internal CA and non public dns zone. So there are extra steps for this. The main one being addition of a host file entry and a ca certificate download to the docker dind container used as a service in the build-docker step.

deploy uses the alpine container which downloads a version of kubectl based on a variable, creates the kube config using certificate authentication and then updates the manifest to generate unique pods, services, ingress, also creates a secret for the registry access. After this it then creates them in kubernetes using the private registry for the image location.

TODO

remove testing commands, add logging during stages, add vCloud NSX Edge configuration script. Add a more secure way of getting client certificates for kube config and use namespace specific ones instead of a big bad global admin. Figure out why I can't add the ca.crt via a variable rather than having to download from an httpd instance.
