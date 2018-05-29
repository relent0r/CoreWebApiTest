# CoreWebApiTest
.net core gitlab ci build

This is a test web api built to test gitlab CI using the docker executor

The .gitlab-ci.yml contains two stages
build-dotnet
build-docker

build-dotnet uses the microsoft dotnet latest container to run the publish command then will upload the resulting binaries to the gitlab server as artifacts

build-docker uses the docker:dind service to build the container using the aspnetcore:2.0 image. Then tag it and push it to the container registry

TODO

complete the registry push(gotta get my ssl config sorted on the registry), remove testing commands, add logging during stages, add kubernetes pod build, add kuberentes ingress build, add vCloud NSX Edge configuration script.
