## Instalando Ruby

1. Baixar instalador

```
$ https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-2.6.6-1/rubyinstaller-devkit-2.6.6-1-x64.exe
```

 1. Clonando o repositório

Temos que clonar o repositório em sua máquina para que possamos visualizar os testes, para isso:

```
$ git clone https://github.com/Francllin/automation-app.git
```

 2. Instalando os pacotes

Após o repositório ser clonado, acesse-o pela linha de comando do seu sistema operacional e estando na raiz do projeto, use o comando:
```
$ gem install bundler
```

Para instalar as gemas utilizadas:
```
$ bundle install --jobs 8
```

Depois de todos os pacotes serem instalados corretamente, podemos executar a interface de testes, via linha de comando, no PATH da raiz do projeto:
```
$ cucumber -p emulador_sauce_android -p samsung_galaxy_s9
```


***

## Links úteis

- [Site oficial Ruby](https://www.ruby-lang.org/pt/)
- [Site oficial Cucumber](https://cucumber.io/)

***
