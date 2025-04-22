---
layout: page
title: Contribuindo para Expresso
description: Descubra como contribuir para o Express.js, incluindo diretrizes para relatar problemas, enviar pull requests, se tornar um colaborador e entender políticas de segurança.
menu: resources
lang: pt-br
redirect_from: ""
---

# Contribuindo para Expresso

### Procurando contribuir para Expressjs.com? Click [here](#expressjs-website-contributing).

Expresso e os outros projetos na organização [expressjs no GitHub](https://github.com/expressjs) são projetos da [OpenJs Foundation](https://openjsf.org/).
Estes projetos são regidos pelas políticas gerais e diretrizes da Fundação Node.js, juntamente com as diretrizes adicionais abaixo.

- [Comitê Técnico](#technical-committee)
- [Guia de contribuição comunitária](#community-contributing-guide)
- [Guia do colaborador](#collaborators-guide)
- [Políticas e procedimentos de segurança](#security-policies-and-procedures)

## Comitê Técnico

O comitê Técnico Expresso é composto por membros do projeto ativos e guia o desenvolvimento e a manutenção do projeto Express. Para obter mais informações, consulte [Expresso Comunidade - Comité Técnico](community.html#technical-committee).

## Guia de contribuição comunitária

<!-- SRC: expressjs/express Contributing.md -->

O objectivo deste documento é criar um processo de contribuição que:

- Encoraja novas contribuições.
- Encoraja os colaboradores a permanecerem envolvidos.
- Evita processos e burocracia desnecessários sempre que possível.
- Cria um processo transparente de tomada de decisão que torna claro como
 contribuidores podem ser envolvidos na tomada de decisão.

### Vocabulário

- Um **Colaborador** é qualquer indivíduo criando ou comentando em um problema ou pull request.
- Um **Committer** é um subconjunto de contribuidores que receberam acesso de escrita ao repositório.
- Um **Capitão do projeto** é o mantenedor principal de um repositório.
- Um **TC (Comitê Técnico)** é um grupo de autores que representa o conhecimento técnico
 necessário para resolver disputas raras.
- Um **Triager** é um subconjunto de contribuidores a quem foi dado acesso de triagem ao repositório.

### Problemas de Registro

Registre um problema para qualquer pergunta ou problema que você possa ter. Em caso de dúvida, registre um problema e
quaisquer políticas adicionais sobre o que incluir serão fornecidas nas respostas. The only
exception is security disclosures which should be sent privately.

Compositores podem direcionar você para outro repositório, solicitar esclarecimentos adicionais e
adicionar os metadados apropriados antes que a issue seja resolvida.

Peço-lhes que sejam corteses e respeitosos. Espera-se que cada participante siga o Código de Conduta do Projeto
.

### Contribuições

Qualquer alteração a recursos deste repositório deve ser feita por meio de pull requests. Isso se aplica a todas as mudanças
em documentação, código, arquivos binários, etc. Mesmo committers a longo prazo e membros do TC devem usar
pull requests.

Nenhum pull request pode ser mesclado sem ser revisado.

Para contribuições não-triviais, os pull requests devem se sentar durante pelo menos 36 horas para garantir que
colaboradores de outros fusos horários tenham tempo de revisão. Também deve ser dada consideração a
fins de semana e outros períodos de férias, para garantir que todos os participantes ativos tenham um tempo razoável para
se envolverem na discussão e no processo de revisão, se desejarem.

O padrão para cada contribuição é que é aceito uma vez que nenhum committer tem uma objeção.
Durante uma revisão, committers também podem solicitar que um colaborador específico que seja mais versado em
uma área em particular dê uma "LGTM" antes que o PR possa ser mesclado. Não há nenhum processo "sign off" adicional
para as contribuições para a terra. Once all issues brought by committers are addressed it can
be landed by any committer.

In the case of an objection being raised in a pull request by another committer, all involved
committers should seek to arrive at a consensus by way of addressing concerns being expressed
by discussion, compromise on the proposed change, or withdrawal of the proposed change.

Se uma contribuição é controversa e os autores não conseguem concordar sobre como levá-la a terra
ou se deve pousar, então deve ser escalada para o TC. TC members should regularly
discuss pending contributions in order to find a resolution. É esperado que apenas uma
pequena minoria de issues seja levada para resolução do TC e que a discussão e o compromisso
entre os committers sejam o mecanismo de resolução padrão.

### Tornando-se um Triager

Qualquer um pode se tornar um triagante! Leia mais sobre o processo de ser um triager em
[o documento do processo de triagem](https://github.com/expressjs/express/blob/master/Triager-Guide.md).

Atualmente, qualquer [membro da organização](https://github.com/orgs/expressjs/people) existente pode nomear
um novo triagador. Se você está interessado em se tornar um triagro, nosso melhor conselho é participar ativamente
na comunidade, ajudando a triplicar problemas e pull requests. Também recomendamos
participar de outras atividades da comunidade, como participar das reuniões do TC, e participar das discussões do Slack
. If you feel ready and have been helping triage some issues, reach out to an active member of the organization to ask if they'd
be willing to support you. Se eles concordarem, podem criar um pull request para formalizar sua nomeação. No caso de uma objecção à nomeação, a equipa de triagem é responsável por trabalhar com as pessoas envolvidas e por encontrar uma resolução.

Você também pode entrar em contato com qualquer um dos [membros da organização](https://github.com/orgs/expressjs/people)
se você tiver dúvidas ou precisar de orientação.

### Tornando-se um Compromissor

Todos os colaboradores que pouparam contribuições significativas e valiosas devem ser integrados em tempo hábil.
e adicionado como um commit, e ser dado acesso de gravação ao repositório.

Espera-se que os compromissos sigam esta política e continuem enviando pull requests, passe por
uma revisão adequada e tenha outros committers que juntem seus pull requests.

### Processo de TC

O TC utiliza um processo de "busca de consenso" para questões que são escaladas para o TC.
O grupo tenta encontrar uma resolução que não tenha objecções abertas entre os membros do TC.
Se um consenso não puder ser alcançado que não tenha objeções, então uma maioria vence a votação
é chamada. Também é esperado que a maioria das decisões tomadas pelo TC sejam via
um consenso procurando processo e que a votação seja usada apenas como um último recurso.

A resolução pode envolver a devolução do problema ao capitão do projeto com sugestões sobre
como avançar em direção a um consenso. Não é esperado que uma reunião do TC
resolva todos os problemas da sua agenda durante essa reunião e talvez prefira continuar
a discussão acontecendo entre os capitães do projeto.

Membros podem ser adicionados à TC a qualquer momento. Qualquer membro do TC pode nomear outro committer
para o TC e o TC usa o seu consenso padrão buscando processo para avaliar se ou
não para adicionar este novo membro. The TC will consist of a minimum of 3 active members and a
maximum of 10. Se o TC deve deixar abaixo de 5 membros, os membros ativos do TC devem nomear
alguém novo. Se um membro do TC estiver parado, eles serão encorajados (mas não é necessário) a
nomear alguém para ocupar o lugar.

Membros da TC serão adicionados como administradores no Github orgs, npm orgs, e outros recursos como
necessários para ser efetivo no papel.

Para permanecer "ativo" um membro do TC deve ter participação nos últimos 12 meses e perder
não mais do que seis reuniões consecutivas de TC. Nosso objetivo é aumentar a participação, não punir
pessoas por qualquer falta de participação, esta diretriz só deve ser usada como tal
(substitua um membro inativo por um novo ativo, por exemplo). Espera-se que os membros que não encontrarem este
se demitam. Se um membro TC não parar, um problema pode ser aberto no repositório
das discussões para movê-lo para o status inativo. Membros TC que desçam ou são removidos devido
à inatividade serão movidos para o status inativo.

Os membros do status inativo podem se tornar membros ativos por auto-nomeação se o TC já não for
maior que o máximo de 10. Eles também receberão preferência se, enquanto estiver no tamanho máximo, um
membro ativo diminui.

### Capitães de Projeto

The Express TC can designate captains for individual projects/repos in the
organizations. Estes capitães são responsáveis por serem os principais mantenedores
do repositório em uma frente técnica e comunitária.
Os capitães do Repo são fortalecidos com propriedade de repositório e direitos de publicação de pacote.
Quando houver conflitos, especialmente em tópicos que afetam o projeto Express
em geral, os capitães são responsáveis por levá-lo para o TC e conduzir
esses conflitos para a resolução. Capitães também são responsáveis por garantir que
membros da comunidade sigam as diretrizes da comunidade. manter o repositório
e o pacote publicado, bem como fornecer suporte ao usuário.

Como os membros do TC, capitães do Repo são um subconjunto de commiters.

Para se tornar um capitão de um projeto, espera-se que o candidato participe daquele projeto
por pelo menos 6 meses como autor do commit antes da solicitação. Eles devem ter
ajudado nas contribuições de código, bem como nos problemas de triagem. They are also required to
have 2FA enabled on both their GitHub and npm accounts.

Qualquer membro do TC ou um capitão existente no repositório **mesmo** pode nomear outro autor
para o papel do capitão. Para isso, eles devem submeter um PR a este documento, atualizando a seção
**Capitães de Projeto Ativos** (mantendo a ordem de classificação) com o nome
, do projeto, o nome de usuário do GitHub e seu nome de usuário npm (se diferente).

- Os repos podem ter tantos capitães quanto fazem sentido para o âmbito do trabalho.
- Um membro do TC ou um repositório existente **no mesmo projeto** pode nomear um novo capitão.
 Os comandantes de repo de outros projectos não devem nomear capitães para um projecto diferente.

O PR exigirá pelo menos 2 aprovações de membros do TC e 2 semanas de tempo em espera para permitir
para comentário e/ou desenviado.  When the PR is merged, a TC member will add them to the
proper GitHub/npm groups.

#### Projetos e Capitães ativos

- [`expressjs/badgeboard`](https://github.com/expressjs/badgeboard): @wesleytodd
- [`expressjs/basic-auth-connect`](https://github.com/expressjs/basic-auth-connect): @ulisesGascon
- [`expressjs/body-parser`](https://github.com/expressjs/body-parser): @wesleytodd, @jonchurch, @ulisesGascon
- [`expressjs/compression`](https://github.com/expressjs/compression): @ulisesGascon
- [`expressjs/connect-multiparty`](https://github.com/expressjs/connect-multiparty): @ulisesGascon
- [`expressjs/cookie-parser`](https://github.com/expressjs/cookie-parser): @wesleytodd, @UlisesGascon
- [`expressjs/cookie-session`](https://github.com/expressjs/cookie-session): @ulisesGascon
- [`expressjs/cors`](https://github.com/expressjs/cors): @jonchurch, @ulisesGascon
- [`expressjs/discussões`](https://github.com/expressjs/discussions): @wesleytodd
- [`expressjs/errorhandler`](https://github.com/expressjs/errorhandler): @ulisesGascon
- [`expressjs/express-paginate`](https://github.com/expressjs/express-paginate): @ulisesGascon
- [`expressjs/express`](https://github.com/expressjs/express): @wesleytodd, @ulisesGascon
- [`expressjs/expressjs.com`](https://github.com/expressjs/expressjs.com): @crandmck, @jonchurch, @bjohansebas
- [`expressjs/flash`](https://github.com/expressjs/flash): @ulisesGascon
- [`expressjs/generator`](https://github.com/expressjs/generator): @wesleytodd
- [`expressjs/method-override`](https://github.com/expressjs/method-override): @ulisesGascon
- [`expressjs/morgan`](https://github.com/expressjs/morgan): @jonchurch, @ulisesGascon
- [`expressjs/multer`](https://github.com/expressjs/multer): @LinusU, @ulisesGascon
- [`expressjs/response-time`](https://github.com/expressjs/response-time): @UlisesGascon
- [`expressjs/serve-favicon`](https://github.com/expressjs/serve-favicon): @ulisesGascon
- [`expressjs/serve-index`](https://github.com/expressjs/serve-index): @ulisesGascon
- [`expressjs/serve-static`](https://github.com/expressjs/serve-static): @ulisesGascon
- [`expressjs/session`](https://github.com/expressjs/session): @ulisesGascon
- [`expressjs/statusboard`](https://github.com/expressjs/statusboard): @wesleytodd
- [`expressjs/timeout`](https://github.com/expressjs/timeout): @ulisesGascon
- [`expressjs/vhost`](https://github.com/expressjs/vhost): @ulisesGascon
- [`jshttp/accepts`](https://github.com/jshttp/accepts): @blakeembrey
- [`jshttp/basic-auth`](https://github.com/jshttp/basic-auth): @blakeembrey
- [`jshttp/compressible`](https://github.com/jshttp/compressible): @blakeembrey
- [`jshttp/content-disposition`](https://github.com/jshttp/content-disposition): @blakeembrey
- [`jshttp/content-type`](https://github.com/jshttp/content-type): @blakeembrey
- [`jshttp/cookie`](https://github.com/jshttp/cookie): @blakeembrey
- [`jshttp/etag`](https://github.com/jshttp/etag): @blakeembrey
- [`jshttp/forwarded`](https://github.com/jshttp/forwarded): @blakeembrey
- [`jshttp/fresh`](https://github.com/jshttp/fresh): @blakeembrey
- [`jshttp/http-assert`](https://github.com/jshttp/http-assert): @wesleytodd, @jonchurch, @ulisesGascon
- [`jshttp/http-errors`](https://github.com/jshttp/http-errors): @wesleytodd, @jonchurch, @ulisesGascon
- [`jshttp/media-typer`](https://github.com/jshttp/media-typer): @blakeembrey
- [`jshttp/methods`](https://github.com/jshttp/methods): @blakeembrey
- [`jshttp/mime-db`](https://github.com/jshttp/mime-db): @blakeembrey, @UlisesGascon
- [`jshttp/mime-types`](https://github.com/jshttp/mime-types): @blakeembrey, @UlisesGascon
- [`jshttp/negotiator`](https://github.com/jshttp/negotiator): @blakeembrey
- [`jshttp/on-finished`](https://github.com/jshttp/on-finished): @wesleytodd, @ulisesGascon
- [`jshttp/on-headers`](https://github.com/jshttp/on-headers): @blakeembrey
- [`jshttp/proxy-addr`](https://github.com/jshttp/proxy-addr): @wesleytodd, @ulisesGascon
- [`jshttp/range-parser`](https://github.com/jshttp/range-parser): @blakeembrey
- [`jshttp/statuses`](https://github.com/jshttp/statuses): @blakeembrey
- [`jshttp/type-is`](https://github.com/jshttp/type-is): @blakeembrey
- [`jshttp/vary`](https://github.com/jshttp/vary): @blakeembrey
- [`pilarjs/cookies`](https://github.com/pillarjs/cookies): @blakeembrey
- [`pilarjs/csrf`](https://github.com/pillarjs/csrf): @ulisesGascon
- [`pilarjs/encodeurl`](https://github.com/pillarjs/encodeurl): @blakeembrey
- [`pillarjs/finalhandler`](https://github.com/pillarjs/finalhandler): @wesleytodd, @ulisesGascon
- [`pilarjs/hbs`](https://github.com/pillarjs/hbs): @ulisesGascon
- [`pilarjs/multiparty`](https://github.com/pillarjs/multiparty): @blakeembrey
- [`pillarjs/parseurl`](https://github.com/pillarjs/parseurl): @blakeembrey
- [`pilarjs/path-to-regexp`](https://github.com/pillarjs/path-to-regexp): @blakeembrey
- [`pilarjs/request`](https://github.com/pillarjs/request): @wesleytodd
- [`pilarjs/resolve-path`](https://github.com/pillarjs/resolve-path): @blakeembrey
- [`pilarjs/roteador`](https://github.com/pillarjs/router): @wesleytodd, @ulisesGascon
- [`pilarjs/enviar`](https://github.com/pillarjs/send): @blakeembrey
- [`pilarjs/understanding-csrf`](https://github.com/pillarjs/understanding-csrf): @ulisesGascon

#### Capitães da Iniciativa Atual

- Equipe de Triage [ref](https://github.com/expressjs/discussions/issues/227): @UlisesGascon

### Certificado de Origem 1.1 do desenvolvedor

```text
By making a contribution to this project, I certify that:

 (a) The contribution was created in whole or in part by me and I
     have the right to submit it under the open source license
     indicated in the file; or

 (b) The contribution is based upon previous work that, to the best
     of my knowledge, is covered under an appropriate open source
     license and I have the right under that license to submit that
     work with modifications, whether created in whole or in part
     by me, under the same open source license (unless I am
     permitted to submit under a different license), as indicated
     in the file; or

 (c) The contribution was provided directly to me by some other
     person who certified (a), (b) or (c) and I have not modified
     it.

 (d) I understand and agree that this project and the contribution
     are public and that a record of the contribution (including all
     personal information I submit with it, including my sign-off) is
     maintained indefinitely and may be redistributed consistent with
     this project or the open source license(s) involved.
```

## Guia do colaborador

<!-- SRC: expressjs/express Collaborator-Guide.md -->

### Problemas no site

Abrir issues para o site expressjs.com em https://github.com/expressjs/expressjs.com.

### Contribuições PRs e Code

- Os testes devem passar.
- Siga o [Estilo Padrão JavaScript](https://standardjs.com/) e o `npm run lint`.
- Se você consertar um bug, adicione um teste.

### Filiais

Use the `master` branch for bug fixes or minor work that is intended for the
current release stream.

Use a branch correspondente nomeada, por exemplo, `5.0`, para qualquer coisa destinada a
uma versão futura do Express.

### Etapas para contribuir

1. [Criar uma issue](https://github.com/expressjs/express/issues/new) para o bug
 que deseja corrigir ou o recurso que deseja adicionar.
2. Crie seu próprio [fork](https://github.com/expressjs/express) no GitHub, e depois
 faça check-out do seu fork.
3. Escreva seu código na sua cópia local. É uma boa prática criar filial para
 cada novo problema no qual você trabalha, embora não seja obrigatório.
4. Para executar o conjunto de testes, primeiro instale as dependências executando `npm install`,
 e então execute `npm test`.
5. Ensure your code is linted by running `npm run lint` -- fix any issue you
 see listed.
6. Se os testes passarem, você poderá confirmar suas alterações no seu fork e, em seguida, criar
 um pull request a partir de lá. Certifique-se de fazer referência a seu problema dos comentários da pull
 request incluindo o número de problema, por exemplo, `#123`.

### Questões que são questões

Normalmente vamos fechar quaisquer problemas vagos ou questões específicas para alguns
app que você está escrevendo. Por favor, verifique a documentação e outras referências antes de
ser acionado o prazer de postar uma questão.

Coisas que ajudarão a examinar o problema da sua pergunta:

- Código JS completo e executável.
- Limpar descrição do problema ou comportamento inesperado.
- Descrição clara do resultado esperado.
- Passos que você levou para depurá-lo você mesmo.

If you post a question and do not outline the above items or make it easy for
us to understand and reproduce your issue, it will be closed.

## Políticas e procedimentos de segurança

<!-- SRC: expressjs/express Security.md -->

Este documento delineia procedimentos de segurança e políticas gerais para o projeto Express
.

- [Relatando um erro](#reporting-a-bug)
- [Política de divulgação](#disclosure-policy)
- [Comentários sobre esta política](#comments-on-this-policy)

### Relatando um Bug

A equipe e comunidade Express levam a sério todos os erros de segurança no Express
Obrigado por melhorar a segurança do Express. Agradecemos seus esforços e
divulgação responsável e faremos todos os esforços para reconhecer suas contribuições
.

Reporte erros de segurança enviando um e-mail para `express-security@lists.openjsf.org`.

Para garantir a resposta oportuna ao seu relatório, por favor, certifique-se de que a totalidade
do relatório é contida dentro do corpo do e-mail e não apenas por trás de um link
web ou um anexo.

O responsável pela manutenção do seu email reconhecerá seu email em 48 horas, e enviará uma
resposta mais detalhada dentro de 48 horas, indicando as próximas etapas no tratamento de
seu relatório. After the initial reply to your report, the security team will
endeavor to keep you informed of the progress towards a fix and full
announcement, and may ask for additional information or guidance.

Reporte erros de segurança em módulos de terceiros para a pessoa ou equipe que mantém
o módulo.

### Versões de pré-lançamento

Versões Alfa e Beta são instáveis e **não são adequadas para uso em produção**.
Vulnerabilidades encontradas em pré-lançamentos devem ser relatadas de acordo com a seção [Reportar um Bug](#reporting-a-bug).
Devido à natureza instável do branch, não está garantido que quaisquer correções serão lançadas na próxima versão pré-lançada.

### Política de Divulgação

When the security team receives a security bug report, they will assign it to a
primary handler. Essa pessoa coordenará o processo de correção e lançamento,
envolvendo as seguintes etapas:

- Confirme o problema e determine as versões afetadas.
- Analise o código para encontrar possíveis problemas semelhantes.
- Preparar correções para todas as versões que ainda estão em manutenção. These fixes will be
 released as fast as possible to npm.

### O Modelo de Ameaça expressa

Estamos trabalhando em uma nova versão do modelo de segurança, a versão mais atualizada pode ser encontrada [here](https://github.com/expressjs/security-wg/blob/main/docs/ThreatModel.md)

### Comentários sobre esta Política

If you have suggestions on how this process could be improved please submit a
pull request.

----

# Contribuindo para Expressjs.com {#expressjs-website-contributing}

<!-- LOCAL: expressjs/expressjs.com ../../CONTRIBUTING.md -->

### A Documentação Oficial do Framework Express JS

Esta é a documentação de contribuição para o site [Expressjs.com](https://github.com/expressjs/expressjs.com).

#### Precisa de algumas ideias? Estas são algumas questões típicas.

1. **Website problemas**:
 Se você ver alguma coisa no site que possa usar um tune-up, pense em como corrigi-lo.

 - Problemas de exibição ou tamanho de tela
 - Problemas de resposta móvel
 - Recursos de acessibilidade inexistentes ou danificados
 - Rotinas do website
 - Links quebrados
 - Estrutura de página ou aprimoramentos de interface de usuário

2. **Problemas de conteúdo**:
 Corrija tudo relacionado ao conteúdo ou erros de digitação do site.
 - SOrtografia de erros
 - Documentação Express JS incorreta/desatualizada
 - Conteúdo ausente

3. **Problemas de tradução**: corrigir quaisquer erros de tradução ou contribuir com novo conteúdo.
 - Corrigir erros ortográficos
 - Corrigir palavras traduzidas incorretamente/mal
 - Traduzir novo conteúdo

> **IMPORTANTE:**
> Todas as submissões de tradução estão pausadas. Veja este [notice](#notice-we-have-paused-all-translation-contributions) para mais informações.

- Confira a seção [Traduções colaborativas](#contributing-translations) abaixo para um guia de contribuição.

#### Quer trabalhar em uma tarefa em atraso?

Muitas vezes temos bugs ou aprimoramentos que precisam de trabalho. Você pode encontrá-los sob a [guia Problemas] de nosso repositório (https://github.com/expressjs/expressjs.com/issues). Confira as tags para encontrar algo que seja um bom jogo para você.

#### Tem uma ideia? Encontrou um bug?

Se você encontrou um bug ou um erro de digitação, ou se você tem uma ideia para um aprimoramento, você pode:

- Envie um [novo problema](https://github.com/expressjs/expressjs.com/issues/new/choose) em nosso repositório. Faça isto para maiores propostas, ou se você gostaria de discutir ou receber um feedback primeiro.
- Make a [Github pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request). Se você já fez trabalho e está pronto para ir, sinta-se à vontade para enviá-lo pelo nosso caminho.

## Introdução

Os passos abaixo guiarão você através do processo de contribuição do Expressjs.com.

#### Passo 1: (OPCIONAL) Abra uma nova issue

Então você encontrou um problema que deseja corrigir, ou tem um aprimoramento de site que deseja fazer.

1. Se você deseja receber feedback ou discutir, abra uma discussão [issue](https://github.com/expressjs/expressjs.com/issues/new/choose) antes de iniciar o trabalho. Isso não é necessário, mas sim encorajado a apresentar propostas de maior envergadura.
 - Embora encorajemos fortemente esta medida, ela destina-se apenas a apresentação de propostas de mudança significativa. Ajuda-nos a clarificar e concentrar o trabalho e a assegurar que este esteja em sintonia com as prioridades gerais dos projectos.
 - Para as submissões que propõem pequenas melhorias ou correcções, isso não é necessário. Você pode pular esta etapa.
 - Ao abrir uma questão, por favor dê um título e preencha a seção de descrição. Quanto mais detalhes você fornecer, mais feedback nós podemos dar.

2. Depois de receber seu problema, a equipe de documentação Express JS responderá com feedback. Nós lemos todas as submissões e sempre tentamos responder rapidamente com comentários.
 - Para submissões propondo alterações significativas, recomendamos que você siga o processo de revisão antes de iniciar o trabalho.

#### Passo 2: Obtenha a Base do Código de Aplicação

Clonar o repositório e obter o código:

```
git clone https://github.com/expressjs/expressjs.com.git
```

Depois de ter o código você está pronto para começar a fazer as alterações!

Mas só para o caso de você precisar de uma explicação extra, esta seção abaixo descreve as seções principais da base de código, onde a maioria das alterações provavelmente serão feitas.

**Arquivos de Página Markdown**:

- Esses arquivos são renderizados para html e compõem as páginas individuais do site. A maioria do conteúdo de texto da documentação do site está escrita em arquivos 'md'.
- Altera-os para fazer alterações no conteúdo/texto ou markup de páginas individuais.
- Cada linguagem tem seu próprio conjunto completo de páginas, localizado sob os respectivos diretórios de idiomas - todo o conteúdo espanhol em markdown é encontrado no diretório `es`, por exemplo.

**Inclui partes e modelos de layout**

- '_includes' são partes que são importados e reutilizados em várias páginas.
 - Estes são usados para importar conteúdo de texto para reutilização em páginas, como a documentação da API, e. ., `_includes > api > en > 5x`, que está incluído em cada idioma.
 - Estes são usados para incluir componentes de página que compõem a interface de usuário e a estrutura da periferia, por exemplo, cabeçalho, rodapé, etc.
- `_layouts` são os modelos usados para encapsular as páginas individuais do site.
 - Estas são usadas para exibir a estrutura da periferia do site, como o cabeçalho e o rodapé, e para injetar e exibir páginas individuais markdown dentro da tag `content`.

**Arquivos Markdown do blog**

- Esses arquivos compõem os posts individuais do blog. Se você quiser contribuir com um post de blog, por favor
 siga as instruções específicas sobre [Como escrever um post de blog.](https://expressjs.com/en/blog/write-post.html)
- Localizado sob o diretório `_posts`.

**CSS or Javascript**

- Todos os arquivos css e js são mantidos nas pastas `css` e `js` na raiz do projeto.

O site Express JS é compilado usando [Jeykyll](https://jekyllrb.com/) e está hospedado em [Github Pages](https://pages.github.com/).

#### Passo 3: Executando o Aplicativo

Agora você precisará de uma maneira de ver suas mudanças, o que significa que você precisará de uma versão em execução do aplicativo. Você tem duas opções.

1. **Executar Locally**: Esta versão local do aplicativo fica ligada e funcionando na sua máquina. Siga nosso [Guia de configuração local](https://github.com/expressjs/expressjs.com?tab=readme-ov-file#local-setup) para usar esta opção.
 - Esta é a opção recomendada para trabalho moderado a complexo.
2. **Run using Deploy Preview**: Use esta opção se você não quiser se preocupar com uma instalação local. Parte do nosso pipeline de integração contínua inclui [Netlify Deploy Preview](https://docs.netlify.com/site-deploys/deploy-previews/).
 1. Para usar isso, você precisará ter suas alterações online - após fazer seu primeiro commit no seu branch de recursos, faça um pull request _rascunho_.
 2. Depois que os passos de compilação forem concluídos, você terá acesso a uma aba **Deploy Preview** que executará suas alterações na web, recompila após fazer push em cada commit.
 3. Depois que você terminar completamente seu trabalho e estiver pronto para revisão, remova o status de rascunho do seu pull request e envie seu trabalho.

## Traduções contributivas

#### Aviso: Pausamos todas as contribuições de tradução.

> **IMPORTANT:**
> We are currently working toward a more streamlined translations workflow. Enquanto este aviso for publicado, nós _não_ aceitaremos quaisquer envios de tradução.

Nós encorajamos fortemente a comunidade de traduções! Nós não temos mais traduções profissionais, e acreditamos no poder de nossa comunidade para fornecer traduções precisas e úteis.

A documentação é traduzida para esses idiomas:

- Inglês (`en`)
- Espanhol (`es`)
- Francês (`fr`)
- Italiano (`it`)
- Indonésio (`id`)
- Japonês (`ja`)
- Coreano (`ko`)
- Português do Brasil (`pt-br`)
- Russo (`ru`)
- Slovak (`sk`)
- Tailandês (`th`)
- Turco (`tr`)
- Ucraniano (`uk`)
- Uzbek (`uz`)
- Chinês simplificado (`zh-cn`)
- Chinês Tradicional (`zh-tw`)

### Adicionando novas traduções completas do site

Se você encontrar uma tradução está faltando na lista, você pode criar uma nova.

Para traduzir Expressjs.com para um novo idioma, siga estas etapas:

1. Clone o repositório [`expressjs.com`](https://github.com/expressjs/expressjs.com).
2. Crie um diretório para o idioma de sua escolha usando seu [código ISO 639-1](https://www.loc.gov/standards/iso639-2/php/code_list.php) como seu nome.
3. Copie `index.md`, `api.md`, `starter/`, `guide/`, `advanced/`, `resources/`, `4x/`, e `3x/`, para o diretório de idiomas.
4. Remova o link para documentos 2.x do menu "API de referência".
5. Atualiza a variável `lang` nos arquivos markdown copiados.
6. Atualizar a variável `title` nos arquivos markdown copiados.
7. Crie o arquivo de cabeçalho, rodapé, aviso e anúncio para o idioma no diretório `_includes/`, nos respectivos diretórios e fazer edições necessárias ao conteúdo.
8. Crie o arquivo de anúncio para o idioma no diretório `_includes/`.
9. Certifique-se de anexar `/{{ page.lang }}` a todos os links do site.
10. Atualize os arquivos [CONTRIBUTING.md](https://github.com/expressjs/expressjs.com/blob/gh-pages/CONTRIBUTING.md#contributing-translations) e `.github/workflows/translation.yml` com a nova linguagem.

### Adicionando Página e Seção Traduções

Muitas traduções do site ainda estão faltando páginas. Para encontrar com quais precisamos de ajuda, você pode [filtrar por merge PRs](https://github.com/expressjs/expressjs.com/pulls?q=is%3Apr+is%3Aclosed+label%3Arequires-translation-es) que inclua a tag para o seu idioma. tal como `requires-translation-es` para requer tradução espanhola.

Se você contribui com uma página ou tradução de seção, por favor consulte o PR. Isso ajuda a pessoa a mesclar a sua tradução para remover a tag da versão original de PR.
