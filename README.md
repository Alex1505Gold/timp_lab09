<h1>Отчет по лобораторной 09</h1>
</br>gmail почта - sgolenkov2002@gmail.com </br>
telegram - @Xacker_ducker

<h2>Ход выполнения лабораторной работы:</h2>

[репозиторий lab09](https://github.com/Alex1505Gold/lab09)</br>
Были выплнены следующие команды
```shell
export GITHUB_TOKEN=мой токен
export GITHUB_USERNAME=Alex1505Gold
export PACKAGE_MANAGER=apt-get
export GPG_PACKAGE_NAME=gpg
$PACKAGE_MANAGER install xclip
alias gsed=sed
alias pbcopy='xclip -selection clipboard'
alias pbpaste='xclip -selection clipboard -o'
cd ${GITHUB_USERNAME}/workspace
pushd .
source scripts/activate
go get github.com/aktau/github-release
git clone https://github.com/${GITHUB_USERNAME}/lab08 projects/lab09
cd projects/lab09
git remote remove origin
git remote add origin https://github.com/${GITHUB_USERNAME}/lab09
gsed -i 's/lab08/lab09/g' README.md
$PACKAGE_MANAGER install ${GPG_PACKAGE_NAME}
gpg --list-secret-keys --keyid-format LONG
gpg --full-generate-key
gpg --list-secret-keys --keyid-format LONG
gpg -K ${GITHUB_USERNAME}
GPG_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep ssb | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')
GPG_SEC_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep sec | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')
gpg --armor --export ${GPG_KEY_ID} | pbcopy
pbpaste
open https://github.com/settings/keys
git config user.signingkey ${GPG_SEC_KEY_ID}
git config gpg.program gpg
test -r ~/.bash_profile && echo 'export GPG_TTY=$(tty)' >> ~/.bash_profile
echo 'export GPG_TTY=$(tty)' >> ~/.profile
cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
cmake --build _build --target package
travis login --auto
travis enable
git tag -s v0.1.0.0
git tag -v v0.1.0.0
git show v0.1.0.0
git push origin master --tags
github-release --version
github-release info -u ${GITHUB_USERNAME} -r lab09
github-release release \
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "libprint" \
    --description "my first release"
export PACKAGE_OS=`uname -s` PACKAGE_ARCH=`uname -m` 
export PACKAGE_FILENAME=print-${PACKAGE_OS}-${PACKAGE_ARCH}.tar.gz
github-release upload \
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "${PACKAGE_FILENAME}" \
    --file _build/*.tar.gz
github-release info -u ${GITHUB_USERNAME} -r lab09
wget https://github.com/${GITHUB_USERNAME}/lab09/releases/download/v0.1.0.0/${PACKAGE_FILENAME}
tar -ztf ${PACKAGE_FILENAME}
```
Также по ходу выполнения было необходимо устоновить go
</br>
Это было сделано при помощи команды
```shell
sudo apt-get install golang-go
```
</br>

Прикрепить скриншоты результатов выполнения команд, к сожалению, не могу, так как на них видны части ключей, что не безопасно 
