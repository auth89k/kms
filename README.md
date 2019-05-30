# linux-kms-server
Linux kms server.

## Run

- With Docker:
```
$ docker run --name kms -it -d -p 1688:1688 insilicosp/vlmcsd
```

- With linux:
```
$ make
$ ./vlmcsd
```

## Ciente usage:

**Note: run `cmd` with administrator.**

- Windows:
```powershell
slmgr /upk
slmgr /ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX
slmgr /skms YOUR_IP_OR_HOSTNAME
slmgr /ato
```

- Office:
```powershell
CD \Program Files\Microsoft Office\Office16 OR CD \Program Files (x86)\Microsoft Office\Office16
cscript ospp.vbs /sethst:YOUR_IP_OR_HOSTNAME
cscript ospp.vbs /inpkey:xxxxx-xxxxx-xxxxx-xxxxx-xxxxx
cscript ospp.vbs /act
cscript ospp.vbs /dstatusall
```

# 시작 프로그램 설정
	A. 서비스 파일 생성
		vi /etc/systemd/system/kms.service

		[Unit]	
		Wants=docker.service
		After=docker.service
		
		[Service]
		RemainAfterExit=yes
		ExecStart=/usr/bin/docker run --name kms -it -d -p 1688:1688 insilicosp/vlmcsd
		ExecStop=/usr/bin/docker stop kms
		
		[Install]
		WantedBy=multi-user.targe
	B. 데몬 재시작
		systemctl daemon-reload
	C. 시작 프로그램 등록
    	systemctl enable kms.service

- Source Code:
You can download source code on [https://forums.mydigitallife.info/threads/50234-Emulated-KMS-Servers-on-non-Windows-platforms](https://forums.mydigitallife.info/threads/50234-Emulated-KMS-Servers-on-non-Windows-platforms)

- Key:
You can find key on [https://technet.microsoft.com/en-us/library/jj612867.aspx](https://technet.microsoft.com/en-us/library/jj612867.aspx)
