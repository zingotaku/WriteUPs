O primeiro desafio que vamos fazer, vai ser um BOF do narnia, vamos começar...

##

Primeiramente, vamos nos conectar ao ssh da máquina usando "ssh narnia0@narnia.labs.overthewire.org -p2226"
a senha é narnia0

##

pronto, entramos, o desafio fica em /narnia, dando um cd /narnia, entramos no diretorio de desafios
Agora, vamos completar o narnia0

##

Dando uma analisada no código de narnia0.c, encontramos a seguinte coisa:
<img src="https://imgur.com/a/dg57PKq" width="60%"><br><br>
Lendo o código, percebemos alguams coisas como: temos a va1, que recebe o valor "0x41414141"
e também a 0xdeadbeef, se o programa receber a 0xdeadbeef, a gente ganha uma shell em /bin/sh
porém, o programa sempre, sempre retorna 0x41414141, dando mais uma lida no código, percebemos que o sistema aguenta sómente 24 bytes, ou seja... Se ocuparmos todos os 24 bytes, não vai ter como fazer a verificação do código, e assim podemos alterar o ret para ele retornar 0xdeadbeef!
Vamos rodar "aaaaaaaaaaaaaaaaaaaaaaaa" (24 a's) e ver o que ele retorna!
Ele retornou o seguinte:
https://imgur.com/a/LMvMFl7
retornou 0x61616161, vamos deixar 4 bytes reservados para o nosso bof. Vou rodar com xxxx no final para ver se ele retorna outro buf.
uepolas
https://imgur.com/a/eSq0Qqi
ele retornou outro valor, então, se enviarmos assembly em hex, "xef\xeb\xda\xde", pela lógica ele vai nos retornar 0xdeadbeef. vamos testar?
vamos usar o comando python -c 'print("a" * 20 "\xef\xbe\xad\xde")' para pegar o codigo.
aaaaaaaaaaaaaaaaaaaaﾭސ⏎

tcharam!!
https://imgur.com/a/1wOJFXX
conseguimos a shell, primeiro desafio concluido, mais tarde postarei mais desafios!


0xdeadbeef