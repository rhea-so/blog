# atlantis 시도기

[https://www.runatlantis.io/](https://www.runatlantis.io/)

atlantis는 Git의 pull request로 terraform을 배포할 수 있도록 도와주는 도구입니다.

즉, Git에서 terraform plan과 apply를 실행할 수 있다는 것입니다!

여러 pull request들간의 충돌도 사전 감지해서 문제를 방지해주며,

쉽고 편하게 terraform 코드와 tfstate를 관리할 수 있다는 장점이 있습니다.

-----

## 맛보기

![ec2](./images/ec2.png)

atlantis를 설치할 EC2를 생성했습니다.

os는 ubuntu 20 입니다

### atlantis 설치

```sh
wget https://github.com/runatlantis/atlantis/releases/download/v0.18.2/atlantis_linux_amd64.zip
mv atlantis_linux_amd64.zip atlantis.zip
sudo apt-get install unzip
unzip atlantis.zip
rm -rf atlantis.zip

./atlantis testdrive
```

![](./images/install-atlantis.png)

[https://github.com/AyameNakiri/atlantis-example/pull/1](https://github.com/AyameNakiri/atlantis-example/pull/1)

```sh
sudo mv ./atlantis /user/local/bin/atlantis


atlantis server --gh-token="GITHUB ACCESS KEY" --gh-user="AyameNakiri" --repo-allowlist="github.com/rhea-so-lab/*" --repo-config=atlantis.yaml --enable-policy-checks --automerge
```

```yml
# atlantis.yaml
policies:
  conftest_version: 0.23.0
  owners:
    users:
    - qwer
  policy_sets:
  - name: null_resource_warning
    path: /home/ubuntu/null_resource_warning/
    source: local
```

[https://turtle1000.tistory.com/99](https://turtle1000.tistory.com/99)

[​https://www.runatlantis.io/docs/configuring-webhooks.html#github-github-enterprise](​https://www.runatlantis.io/docs/configuring-webhooks.html#github-github-enterprise)

![](./images/webhook.png)

[https://github.com/rhea-so-lab/Infrastructure-as-Code/pull/8](https://github.com/rhea-so-lab/Infrastructure-as-Code/pull/8)

-----

## 도전

### aws cli 설치

```sh
sudo apt-get install awscli
aws configure
```

### terraform 설치

[https://learn.hashicorp.com/tutorials/terraform/install-cli](https://learn.hashicorp.com/tutorials/terraform/install-cli)

![install-terraform](./images/install-terraform.png)

![terraform-login](./images/terraform-login.png)

### ec2 생성 해보기

[https://github.com/rhea-so-lab/Infrastructure-as-Code/pull/12](https://github.com/rhea-so-lab/Infrastructure-as-Code/pull/12)

![](./images/pr_1.png)

![](./images/pr_2.png)

![](./images/pr_3.png)

![](./images/pr_4.png)

![](./images/pr_5.png)

![](./images/ssh.png)

[https://github.com/rhea-so-lab/Infrastructure-as-Code/pull/13](https://github.com/rhea-so-lab/Infrastructure-as-Code/pull/13)

![](./images/pr_6.png)

![](./images/pr_7.png)

![](./images/pr_8.png)

![](./images/pr_9.png)

```system
[Unit]
Description=Atlantis Server

[Service]
Type=simple
ExecStart=/home/ubuntu/run_atlantis.sh
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

![](./images/systemctl.png)

systemctl 에 등록해서 터미널에 나가더라도 Atlantis Server는 계속 실행되도록 조치함

​[https://chhanz.github.io/linux/2019/01/18/linux-how-to-create-custom-systemd-service/](https://chhanz.github.io/linux/2019/01/18/linux-how-to-create-custom-systemd-service/)

[https://registry.terraform.io/providers/hashicorp/aws/latest/docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
