Install-Module DockerMsftProvider -Force

Install-Package Docker -ProviderName DockerMsftProvider -Force

invoke-webrequest -UseBasicparsing -Outfile docker-17.06.2-ee-7.zip

Expand-Archive docker-17.06.2-ee-7.zip -DestinationPath $Env: ProgramFiles

Remove-Item -Force docker-17.06.2-ee-7.zip

$null = Install-WindowsFeature containers

$env:path += ";$env:ProgramFiles\docker"

dockerd --register-service

Start-Service docker

docker container run hello-world:nanoserver
