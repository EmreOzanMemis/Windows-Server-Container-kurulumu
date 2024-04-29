# Windows-Server-Container-kurulumu

<div>Windows Server 2016 ile hayatımıza giren container özelliğinden sizlere biraz bahsetmek ve Windows Server 2019 üzerinde container teknolojisinin öncüsü olan docker kurulumunun nasıl yapacağınızı size anlatmak isterim. Sanallaştırma teknolojisinin ardından
        gündemimize hızlı bir giriş yapan container mimarisi özelikle yazılımcıların çok kısa sürede vazgeçilmesi olmaya başlamıştır. Aynı işletim sistemi içerisinde aynı kaynakları kullanarak oluşturulan ve ihtiyaç durumunda kaynakların çok rahat azaltılarak yada
        arttırılabilen bir alt yapıya sahip olan container teknolojisi kendi dosya sistemi, registry ve ağ adreslerine sahip olabildiği için diğer uygulamalardan da izole bir şekilde çalışma imkanı sunmaktadır. Esnek kullanım yapısı ile uygulama geliştiricilerin tercih
        sebebi olmuştur. Peki bu container role kurulumu nasıl yapılır sunucuda nasıl aktif edilir birlikte bakalım. Container role kurulumunu docker ile eş zamanlı sizlere anlatmaya çalışacağım.
        <br>
        </div>
        <div><br>
        </div>
        <div><strong><a href="https://social.technet.microsoft.com/wiki/cfs-file.ashx/__key/communityserver-wikis-components-files/00-00-00-00-05/8228.container.jpeg"><img alt="" src="https://social.technet.microsoft.com/wiki/resized-image.ashx/__size/550x0/__key/communityserver-wikis-components-files/00-00-00-00-05/8228.container.jpeg" style="border-width: 0px; border-style: solid;"></a><br>
        </strong></div>
        <div><strong><br>
        </strong></div>
        <div><strong>Docker EE Kurulumu </strong><br>
        </div>
        <div><br>
        </div>
        <div>Modul kurulumu için "Install-Module" komutu ile kuruluma başlıyoruz. <br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Install-Module DockerMsftProvider -Force</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; Install-Module DockerMsftProvider -Force</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">NuGet provider is required to continue</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">NuGet-based repositories. The NuGet provider must be available in 'C:\Program</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Files\PackageManagement\ProviderAssemblies' or</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">'C:\Users\Administrator\AppData\Local\PackageManagement\ProviderAssemblies'. You can</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">also install the NuGet provider by running 'Install-PackageProvider -Name NuGet</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">-MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">NuGet provider now?</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">[Y] Yes&nbsp; [N] No&nbsp; [S] Suspend&nbsp; [?] Help (default is "Y"):Y</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>Docker paketlerini yüklemek için "Install-Package" komutunu kullanıyoruz. <br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Install-Package Docker -ProviderName DockerMsftProvider -Force</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; Install-Package Docker -ProviderName DockerMsftProvider -Force</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">WARNING: A restart is required to enable the containers feature. Please restart your machine.</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Version&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Source&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Summary</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">----&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; -------&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ------&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; -------</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Docker&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 18.09.4&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; DockerDefault&nbsp;&nbsp;&nbsp; Contains Docker EE ...</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div><br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; docker container run hello-world:nanoserver</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Unable to find image 'hello-world:nanoserver' locally</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">nanoserver: Pulling from library/hello-world</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">6a5e981230da: Pull complete</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">dc4b656f6979: Pull complete</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">2848c5402b33: Pull complete</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">9e0171b11ac8: Pull complete</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Digest: sha256:ea56d430e69850b80cd4969b2cbb891db83890c7bb79f29ae81f3d0b47a58dd9</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Status: Downloaded newer image for hello-world:nanoserver</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Hello from Docker!</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">This message shows that your installation appears to be working correctly.</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">To generate this message, Docker took the following steps:</code></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">1. The Docker client contacted the Docker daemon.</code></span></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">2. The Docker daemon pulled the "hello-world" image from the Docker Hub.</code></span></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><span style="margin-left: 12px !important;"><code style="color: #000000;">(windows-amd64, nanoserver-1809)</code></span></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">3. The Docker daemon created a new container from that image which runs the</code></span></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><span style="margin-left: 12px !important;"><code style="color: #000000;">executable that produces the output you are currently reading.</code></span></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">4. The Docker daemon streamed that output to the Docker client, which sent it</code></span></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><span style="margin-left: 12px !important;"><code style="color: #000000;">to your terminal.</code></span></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">To try something more ambitious, you can run a Windows Server container with:</code></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">PS C:\&gt; docker run -it mcr.microsoft.com/windows/servercore powershell</code></span></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Share images, automate workflows, and more with a free Docker ID:</code></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;"><a href="https://hub.docker.com/">https://hub.docker.com/</a></code></span></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">For more examples and ideas, visit:</code></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;"><a href="https://docs.docker.com/get-started/">https://docs.docker.com/get-started/</a></code></span></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>Script kullanarak Docker EE Kurulumu <br>
        </div>
        <div><br>
        </div>
        <div>Docker kurulumunu Windows Core üzerinde yapacaksanız özelikle size çok faydalı olacak aşağıdaki komutları kullanabilirsiniz. Öncesinde Docker.com üzerinden ilgili paketlerimizi indiriyoruz.
        <br>
        </div>
        <div><br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; invoke-webrequest -UseBasicparsing -Outfile docker-17.06.2-ee-7.zip
        <a href="https://download.docker.com/components/engine/windows-server/17.06/docker-17.06.2-ee-7.zip">
        https://download.docker.com/components/engine/windows-server/17.06/docker-17.06.2-ee-7.zip</a></code></span></div>
        </div>
        <br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Windows PowerShell</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Copyright (C) Microsoft Corporation. All rights reserved.</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">Writing web request</code></span></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><span style="margin-left: 12px !important;"><code style="color: #000000;">Writing request stream... (Number of bytes written: 8431026)</code></span></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>İndirdiğimiz zip dosyasını açarak iligli dizine kaydetmek için aşağıdaki komutumuzu kullanıyoruz.
        <br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; Expand-Archive docker-17.06.2-ee-7.zip -DestinationPath $Env: ProgramFiles</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>İndirdiğimiz zip dosyasını silmek için&nbsp;</div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; Remove-Item -Force docker-17.06.2-ee-7.zip</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>Container role yüklemek için <br>
        </div>
        <div><br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; $null = Install-WindowsFeature containers</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>Yükleniyor...<br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Windows PowerShell</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Copyright (C) Microsoft Corporation. All rights reserved.</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">Start Installation...</code></span></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><span style="margin-left: 12px !important;"><code style="color: #000000;">26%</code></span></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><span style="margin-left: 12px !important;"><code style="color: #000000;">[ooooooooooooooooooo&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ]</code></span></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt;
        </code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; $null = Install-WindowsFeature containers</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>Yükleme tamamlandı. Sistemi yeninden başlatmanız gerekiyor. <br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; $null = Install-WindowsFeature containers</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">WARNING: You must restart this server to finish the installation process.</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>Sistemi yeniden başlattıktan sonra docker servislerini çalıştırıyoruz.</div>
        <div><br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Windows PowerShell</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Copyright (C) Microsoft Corporation. All rights reserved.</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; $env:path += ";$env:ProgramFiles\docker"</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt;</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; dockerd --register-service</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt;</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; Start-Service docker</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt;</code></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>Son olarak docker çalıştırıyoruz. <br>
        </div>
        <div><br>
        </div>
        <div>
        <div class="reCodeBlock" style="border: 1px solid #7f9db9; overflow-y: auto;">
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">PS C:\Users\Administrator&gt; docker container run hello-world:nanoserver</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Unable to find image 'hello-world:nanoserver' locally</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">nanoserver: Pulling from library/hello-world</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">6a5e981230da: Pull complete</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">dc4b656f6979: Pull complete</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">2848c5402b33: Pull complete</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">9e0171b11ac8: Pull complete</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Digest: sha256:ea56d430e69850b80cd4969b2cbb891db83890c7bb79f29ae81f3d0b47a58dd9</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Status: Downloaded newer image for hello-world:nanoserver</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Hello from Docker!</code></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">This message shows that your installation appears to be working correctly.</code></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">To generate this message, Docker took the following steps:</code></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">1. The Docker client contacted the Docker daemon.</code></span></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">2. The Docker daemon pulled the "hello-world" image from the Docker Hub.</code></span></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><span style="margin-left: 12px !important;"><code style="color: #000000;">(windows-amd64, nanoserver-1809)</code></span></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">3. The Docker daemon created a new container from that image which runs the</code></span></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><span style="margin-left: 12px !important;"><code style="color: #000000;">executable that produces the output you are currently reading.</code></span></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">4. The Docker daemon streamed that output to the Docker client, which sent it</code></span></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;&nbsp;&nbsp;&nbsp;</code><span style="margin-left: 12px !important;"><code style="color: #000000;">to your terminal.</code></span></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">To try something more ambitious, you can run a Windows Server container with:</code></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;">PS C:\&gt; docker run -it mcr.microsoft.com/windows/servercore powershell</code></span></span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;"><code style="color: #000000;">Share images, automate workflows, and more with a free Docker ID:</code></span></div>
        <div style="background-color: #ffffff;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;"><a href="https://hub.docker.com/">https://hub.docker.com/</a></code></span></span></div>
        <div style="background-color: #f8f8f8;"><span style="margin-left: 0px !important;">&nbsp;</span></div>
        <div style="background-color: #ffffff;"><span style="margin-left: 0px !important;"><code style="color: #000000;">For more examples and ideas, visit:</code></span></div>
        <div style="background-color: #f8f8f8;"><span><code>&nbsp;</code><span style="margin-left: 3px !important;"><code style="color: #000000;"><a href="https://docs.docker.com/get-started/">https://docs.docker.com/get-started/</a></code></span></span></div>
        </div>
        </div>
        <div><br>
        </div>
        <div>Kaynak: docker.com<br>
        </div>
