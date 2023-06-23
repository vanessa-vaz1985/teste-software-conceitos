# Sobre o projeto
Este projeto visa reunir alguns conceitos sobre Teste de Software, que podem ser utilizados em qualquer metodologia que você esteja inserido, seja no Ágil ou não.
Utilizei conceitos definidos em: 
- Syllabus: 
    https://bcr.bstqb.org.br/docs/syllabus_ctfl_3.1.1br.pdf
- Livro "Base de conhecimento em teste de software":
    https://amzn.to/3Pwtdmz
- Livro "Qualidade de Software":
    https://amzn.to/3NgzakU
- E em alguns vídeos do Júlio de Lima:
    https://youtu.be/23K3oYiSSYc
    https://www.youtube.com/watch?v=3wtavNon34A&list=PLf8x7B3nFTl1H65q7ozKlZFZjD7X2BZCE


## 1. Tipos de Teste (o que testar): É sobre qual perspectiva do sistema irei abordar em meus testes.
    - Agrupamento de características a serem observadas em um software. 
    - A ISO 25010 define 8 características de um software (as características abaixo possuem subcaracterísticas, que também devem ser observadas):
        - Funcionalidade: Através das Técnicas de Teste, defino quais são os testes que serão executados, definindo as entradas que devem ser fornecidas para cada um, e após o processamento do sistema, devem ser fornecidas as saídas, conforme defini anteriormente (baseando nas Regras de Negócio do sistema). 
        - Confiabilidade: Se determinado Banco de Dados estiver indisponível, todo o restante do sistema ficará indisponível?
        - Usabilidade: O sistema é facilmente utilizado pelo usuário, mesmo sem precisar consultar um Manual do Usuário?
        - Eficiência: O sistema está atendendo aos tempos de resposta esperados para cada cenário?
        - Manutenibilidade: O código do sistema foi construído seguindo boas práticas?
        - Portabilidade: O sistema funciona em vários browsers, conforme definido?
        - Segurança: Existe segurança no tráfego de informações, entre os vários componentes do sistema?
        - Compatibilidade: Determinado microsserviço funciona com as diferentes versões do app?
    - Teste estrutural é outro tipo de teste, que não está na ISO 25010. Este Tipo de Teste tem o objetivo de avaliar se a estrutura do software foi construída de forma satisfatória.
    - Tipo de Teste Baseada em Mudanças, outro tipo de teste, que não está na ISO 25010. Por exemplo, uma Regra de Negócio foi alterada, foi necessária uma alteração no código para atender essa mudança. Portanto, será necessário executar um Teste de Regressão, onde serão executados todos os testes que já foram executados antes, com o objetivo de garantir que os mesmos continuam funcionando após a mudança.


## 2. Níveis de Teste (quando testar): É sobre quanto os componentes do sistema estão conectados.
    - Teste de Componente: Quando executo teste em uma parte do sistema, em um componente, isoladamente.
    - Teste de Integração: Quando executo teste em dois ou mais componentes juntos, integrados, mas ainda com uma parte do sistema mockado, por exemplo.
    - Teste de Sistema: Quando executo teste com todos os componentes do sistema integrados, sem mocks. Também chamado de Teste E2E.
    - Teste de Aceite: Quando o teste é executado por quem vai utilizar o sistema.


## 3. Técnicas de Teste (como testar)
- O objetivo das Técnicas de Teste é ajudar a identificar as condições de teste, os casos de teste e os dados de teste.
- A escolhas das técnicas que devem ser utilizadas, dependem de vários fatores, como complexidade do sistema, dos requisitos, dos riscos, do tempo para testar, dos tipos de defeitos esperados, da própria experiência do testador.
- Algumas técnicas são mais aplicáveis em determinadas situações e níveis de teste. Outras são aplicáveis em todos os níveis de teste.


### 3.1 Técnicas Caixa-preta
- Se concentram nas entradas e saídas do objeto de teste, sem referência a sua estrutura interna.
- Se baseiam em regras de negócio, estórias de usuários...
- São aplicáveis a testes funcionais e não-funcionais.

#### 3.1.1 Particionamento de equivalência
- O particionamento de equivalência divide os dados em partições ou classes de equivalência, levando em conta valores válidos e inválidos.
- Exemplo de Regra de Negócio: Clientes com mais de 10 anos de cadastro tem 10% de desconto.

1. Identificar faixa de valores para as Entradas:

        <= 10

        > 10

2. Conversar com o PO, a fim de verificar se existem novas faixas de valores, desta forma podemos antecipar possíveis problemas:

        < 5             - 0%

        >= 5 e <= 10    - 5%

        > 10            - 10%

3. Definir valores dentro de cada faixa para testar:

        < 5             - 0%    - 2

        >= 5 e <= 10    - 5%    - 7

        > 10            - 10%   - 12

#### 3.1.2 Análise de valor limite
- É uma extensão do particionamento de equivalência.
- Os valores mínimo e máximo de uma partição são seus valores limites.
- Geralmente é uma técnica usada para testar requisitos que exigem um intervalo de números, incluindo datas e horas.
- No exemplo do particionamento de equivalência acima, teríamos:

        < 5             - 0%    - 4

        >= 5 e <= 10    - 5%    - 5, 6, 9, 10

        > 10            - 10%   - 11

#### 3.1.3 Teste de tabela de decisão
- É uma boa forma de registrar regras de negócio complexas de um sistema.
- Devem ser identificadas as possíveis entradas e saídas, e cada uma destas corresponde a uma linha da tabela.
- Cada coluna corresponde a uma combinação de entradas, que resultam em uma saída. Serão os casos de teste que serão executados.

#### 3.1.4 Teste de transição de estado
- Os testes podem ser projetados para cobrir uma sequência típica de estados, para exercitar todos os estados, para exercitar cada transição, para executar sequências específicas de transições ou para testar transições inválidas.

#### 3.1.5 Teste de caso de uso
- Os testes tem o objetivo de exercitar os comportamentos definidos no caso de uso.


### 3.2 Técnicas Caixa-branca
- São baseadas na estrutura interna, no código, na arquitetura...

#### 3.2.1 Teste e cobertura de instruções
- Testa as instruções executáveis do código.

#### 3.2.2 Teste e cobertura de decisão
- Testa as decisões existentes no código.
- Em um if, por exemplo, um teste para o resultado verdadeiro e outro para o falso.


### 3.3 Técnicas baseadas na experiência
- Aproveitam o conhecimento dos desenvolvedores, testadores e usuários para projetar, implementar e executar os testes.
- Frequentemente são combinadas com técnicas de caixa-preta e caixa-branca.

#### 3.3.1 Suposição de erro
- Técnica usada para prever a ocorrência de erros, baseando em coisas como:
    - Como o sistema funcionou no passado;
    - Que tipos de erro tendem a ser cometidos;
    - Falhas ocorridas em outros aplicativos.

#### 3.3.2 Teste exploratório
- Nesta técnica, os testes são informais, ou seja, não são pré-definidos. São modelados, executados, registrados e avaliados durante a execução do teste.
- É útil quando há pouca ou inadequadas especificações ou pouco tempo para testar.
- Pode incorporar o uso de outras técnicas de caixa-preta, caixa-branca e experiência.

#### 3.3.3 Teste baseado em checklist
- Esses checklists podem ser construídos com base na experiência, conhecimento sobre o que é importante para o usuário ou uma compreensão de por que e como o software falha.
- Podem ser criados para dar suporte a vários tipos de teste, inclusive funcional e não-funcional.
