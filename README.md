# Moodle - Ecologuia
Este é um projeto de ambiente de aprendizagem Moodle containerizado com Docker, pronto para desenvolvimento local.

## Pré-requisitos
Antes de começar, certifique-se de ter instalado em sua máquina:

- **Docker** (versão 20.10 ou superior) - [Instruções de instalação](https://docs.docker.com/get-docker/)
- **Docker Compose** (versão 2.0 ou superior) - [Instruções de instalação](https://docs.docker.com/compose/install/)
- **Git** - [Instruções de instalação](https://git-scm.com/downloads)

Para verificar se está tudo instalado corretamente, execute:

```bash
docker --version
docker-compose --version
git --version
```

## Instalação

### 1. Clonar o Repositório
Clone o repositório para sua máquina local:

```bash
git clone https://github.com/seu-usuario/ecologuia.git
cd ecologuia
```

### 2. Construir a Imagem Docker
Construa a imagem Docker do Moodle:

```bash
docker-compose build
```

Este processo pode levar alguns minutos na primeira vez, pois irá:

- Baixar a imagem base do PHP 8.2 com Apache
- Instalar todas as dependências do sistema
- Configurar as extensões PHP necessárias para o Moodle
- Copiar os arquivos da aplicação

### 3. Iniciar os Containers
Inicie os containers em segundo plano:

```bash
docker-compose up -d
```

Aguarde alguns instantes para que o banco de dados seja inicializado. Você pode acompanhar os logs com:

```bash
docker-compose logs -f
```

Pressione `Ctrl+C` para sair da visualização de logs.

## Acessando o Moodle
Após os containers estarem rodando, acesse o Moodle em seu navegador:

**URL:** http://localhost:8080

### Credenciais de Administrador
Use as seguintes credenciais para fazer login como administrador:

- **Usuário:** ecologuia.admin
- **E-mail:** ecologuia.adm@gmail.com
- **Senha:** #$a=lkk+T&4crc0m

⚠️ **Importante:** Altere a senha de administrador após o primeiro acesso em um ambiente de produção.

## Troubleshooting

### Porta 8080 já está em uso
Se você receber um erro informando que a porta 8080 já está em uso, você pode:

1. Parar o serviço que está usando a porta 8080, ou
2. Modificar a porta no arquivo `docker-compose.yml`, alterando a linha `"8080:80"` para outra porta, como `"8081:80"`

### Erro de permissão nos volumes
Se encontrar erros relacionados a permissões de arquivos:

```bash
sudo chown -R $USER:$USER ./app ./moodledata
```

### Container do banco de dados não inicia
Verifique os logs do banco de dados:

```bash
docker-compose logs db
```

Certifique-se de que não há outro serviço MySQL rodando na porta 3306.

### Página em branco ou erro 500
Verifique os logs do container da aplicação:

```bash
docker-compose logs app
```

Certifique-se de que o diretório `app` existe e contém os arquivos do Moodle.

### Problemas com extensões PHP
O projeto já vem configurado com todas as extensões PHP necessárias para o Moodle:

- GD (para processamento de imagens)
- Intl (para internacionalização)
- Zip (para arquivos compactados)
- SOAP (para web services)
- MySQLi (para conexão com banco de dados)
- OPcache (para otimização)
- EXIF (para metadados de imagens)

Se ainda assim encontrar problemas, reconstrua a imagem:

```bash
docker-compose down
docker-compose build --no-cache
docker-compose up -d
```

## Gerenciamento dos Containers

### Verificar status dos containers
```bash
docker-compose ps
```

### Parar os containers
```bash
docker-compose stop
```

### Reiniciar os containers
```bash
docker-compose restart
```

### Parar e remover os containers
```bash
docker-compose down
```

### Remover containers e volumes (⚠️ CUIDADO: apaga todos os dados)
```bash
docker-compose down -v
```

⚠️ **Atenção:** Este comando irá apagar todos os dados do banco de dados e arquivos do Moodle. Use apenas se quiser começar do zero.

## Estrutura do Projeto

```
ecologuia/
├── app/                    # Arquivos do Moodle
├── moodledata/            # Dados persistentes do Moodle
├── docker-compose.yml     # Configuração dos containers
├── Dockerfile            # Imagem Docker customizada
└── README.md             # Este arquivo
```

## Tecnologias Utilizadas

- **PHP 8.2** com Apache
- **MySQL 8.4** com charset UTF-8MB4
- **Moodle** (plataforma de aprendizagem)
- **Docker** e **Docker Compose** para containerização

## Suporte
Para problemas ou dúvidas, consulte a [documentação oficial do Moodle](https://docs.moodle.org/) ou entre em contato com a equipe de desenvolvimento.

---

<p align="center"><a href="https://moodle.org" target="_blank" title="Moodle Website">
  <img src="https://raw.githubusercontent.com/moodle/moodle/main/.github/moodlelogo.svg" alt="The Moodle Logo">
</a></p>

[Moodle][1] is the World's Open Source Learning Platform, widely used around the world by countless universities, schools, companies, and all manner of organisations and individuals.

Moodle is designed to allow educators, administrators and learners to create personalised learning environments with a single robust, secure and integrated system.

## Documentation

- Read our [User documentation][3]
- Discover our [developer documentation][5]
- Take a look at our [demo site][4]

## Community

[moodle.org][1] is the central hub for the Moodle Community, with spaces for educators, administrators and developers to meet and work together.

You may also be interested in:

- attending a [Moodle Moot][6]
- our regular series of [developer meetings][7]
- the [Moodle User Association][8]

## Installation and hosting

Moodle is Free, and Open Source software. You can easily [download Moodle][9] and run it on your own web server, however you may prefer to work with one of our experienced [Moodle Partners][10].

Moodle also offers hosting through both [MoodleCloud][11], and our [partner network][10].

## License

Moodle is provided freely as open source software, under version 3 of the GNU General Public License. For more information on our license see

[1]: https://moodle.org
[2]: https://moodle.com
[3]: https://docs.moodle.org/
[4]: https://sandbox.moodledemo.net/
[5]: https://moodledev.io
[6]: https://moodle.com/events/mootglobal/
[7]: https://moodledev.io/general/community/meetings
[8]: https://moodleassociation.org/
[9]: https://download.moodle.org
[10]: https://moodle.com/partners
[11]: https://moodle.com/cloud
[12]: https://moodledev.io/general/license


### Doc antiga abaixo

# Moodle

<p align="center"><a href="https://moodle.org" target="_blank" title="Moodle Website">
  <img src="https://raw.githubusercontent.com/moodle/moodle/main/.github/moodlelogo.svg" alt="The Moodle Logo">
</a></p>

[Moodle][1] is the World's Open Source Learning Platform, widely used around the world by countless universities, schools, companies, and all manner of organisations and individuals.

Moodle is designed to allow educators, administrators and learners to create personalised learning environments with a single robust, secure and integrated system.

## Documentation

- Read our [User documentation][3]
- Discover our [developer documentation][5]
- Take a look at our [demo site][4]

## Community

[moodle.org][1] is the central hub for the Moodle Community, with spaces for educators, administrators and developers to meet and work together.

You may also be interested in:

- attending a [Moodle Moot][6]
- our regular series of [developer meetings][7]
- the [Moodle User Association][8]

## Installation and hosting

Moodle is Free, and Open Source software. You can easily [download Moodle][9] and run it on your own web server, however you may prefer to work with one of our experienced [Moodle Partners][10].

Moodle also offers hosting through both [MoodleCloud][11], and our [partner network][10].

## License

Moodle is provided freely as open source software, under version 3 of the GNU General Public License. For more information on our license see

[1]: https://moodle.org
[2]: https://moodle.com
[3]: https://docs.moodle.org/
[4]: https://sandbox.moodledemo.net/
[5]: https://moodledev.io
[6]: https://moodle.com/events/mootglobal/
[7]: https://moodledev.io/general/community/meetings
[8]: https://moodleassociation.org/
[9]: https://download.moodle.org
[10]: https://moodle.com/partners
[11]: https://moodle.com/cloud
[12]: https://moodledev.io/general/license
