# Criando-um-Assistente-de-Delivery-com-AWS-Step-Functions-e-Bedrock
Criando um Assistente de Delivery com AWS Step Functions e Bedrock
**Pré-requisitos:**
Antes de começar, é essencial ter uma conta ativa na AWS com permissões adequadas e um entendimento básico sobre AWS. Familiaridade com linguagens como JSON ou YAML para definir fluxos de trabalho também é recomendada.

**Situação Problema:**  
Empresas de entrega enfrentam desafios na coordenação eficiente de pedidos, rastreamento e comunicação entre clientes, entregadores e lojas. Esses processos manuais geralmente resultam em erros, atrasos e falta de transparência.

**AWS Step Functions - Página Oficial:**  
O AWS Step Functions é um serviço para coordenar componentes distribuídos, ideal para automação de fluxos de trabalho complexos. Na página oficial, é possível encontrar visão geral, tutoriais e melhores práticas.

**Documentação Oficial:**  
A documentação do AWS Step Functions traz informações detalhadas sobre a linguagem de definição de fluxos de trabalho, integração com outros serviços AWS, exemplos práticos e APIs para gerenciar tarefas.

**Localizando o Serviço:**  
Acesse o AWS Console e faça login. No AWS Management Console, busque por "Step Functions" e clique no serviço para começar a criar e gerenciar fluxos de trabalho.

**Começando com um Projeto Template:**  
O AWS Step Functions oferece templates prontos para que você inicie projetos rapidamente, abordando casos como automação de processos, pipelines de dados e orquestração de microserviços.

**Workflow Studio & ASL:**  
O Workflow Studio é uma ferramenta visual que permite criar, editar e visualizar fluxos de trabalho de forma intuitiva, com funcionalidades de arrastar e soltar. Isso facilita a construção de workflows complexos, permitindo configurar estados e interações com outros serviços AWS.  
A Amazon States Language (ASL) é baseada em JSON e define os estados e transições dos workflows no Step Functions, conectando etapas e ações de cada estado.  

**Componentes:**
- **Ações:**
  - **Tarefas:** Executam uma função específica, como rodar uma função Lambda, chamar uma API, ou integrar um serviço externo.
  - **Escolhas:** Condicionais (if/else) que decidem o próximo estado com base em variáveis.
  - **Espera:** Pausa o fluxo por um tempo determinado.
  - **Sucesso/Falha (Succeed/Fail):** Define um estado como sucesso ou falha, encerrando o workflow.
- **Fluxo:**
  - **Sequência:** Ordena ações para ocorrerem numa sequência específica.
  - **Mapeamento:** Executa uma ação repetidamente para cada item de uma lista.
  - **Paralelo:** Executa ações simultaneamente, avançando apenas quando todas são concluídas.
- **Padrões:**
  - **Orquestração Sequencial:** As ações seguem uma ordem, passando de um estado ao outro conforme os resultados.
  - **Orquestração Paralela:** Várias ações ocorrem ao mesmo tempo, e o fluxo só avança quando todas terminam.
  - **Ramificação:** O fluxo segue caminhos diferentes com base nas condições definidas nos estados de escolha.

**Criando um Hello World:**  
Esse exemplo básico em Step Functions é um fluxo simples que executa funções e permite personalizar nomes, tipo de estado, próximo estado e comentários, retornando uma mensagem de sucesso. Esse projeto demonstra conceitos fundamentais de estados, transições e integração do Step Functions com outros serviços AWS.

**Precificação e Custos:**  
O AWS Step Functions é cobrado pelo número de transições de estado nos fluxos. O custo depende do volume e complexidade das execuções, além dos custos dos serviços AWS integrados ao fluxo. **Dica:** Exclua a máquina de estados após o uso para evitar cobranças indesejadas.

**Configuração - Nível 1: Permissão de Perfil**  
Configure permissões para o usuário e os serviços envolvidos, geralmente criando papéis (roles) no IAM para que o Step Functions tenha as permissões adequadas para invocar outros serviços AWS.

**Configuração - Nível 2: Disponibilidade de Serviço**  
Esse nível trata da disponibilidade dos serviços integrados ao Step Functions, garantindo que os recursos estejam distribuídos de forma a evitar falhas.

**Criando um Assistente de Delivery na Prática:**  
Nesse fluxo de trabalho, implementa-se um assistente de delivery, onde o Step Functions coordena serviços para o gerenciamento de pedidos.

**Passo a Passo:**
1. **Criar a Máquina de Estados:** No AWS Step Functions, clique em "Criar máquina de estados", escolha o modelo desejado, selecione "Implantar e Executar". Para ajustar o workflow, clique em "Cancelar" e depois em "Editar".
2. **Configurar Permissões (Nível 1):** Na tela de design, vá para "Configurações", clique em "Visualizar no IAM" e adicione as permissões necessárias. Retorne à tela de Design.
   - **Exemplo de comando para adicionar permissões via CLI:**
     ```shell
     aws iam attach-role-policy --role-name StepFunctionsRole --policy-arn arn:aws:iam::aws:policy/service-role/AWSStepFunctionsFullAccess
     ```
3. **Selecionar os Modelos:** Selecione blocos ou estados apropriados para o workflow (Task, Pass, etc.) e ajuste conforme necessário.
4. **Configurar o Bloco de Entrada:** Na configuração do bloco de entrada, aumente o número de tokens se necessário.
   ```json
   {
     "Type": "Task",
     "Resource": "arn:aws:lambda:us-east-1:123456789012:function:MyFunction",
     "ResultPath": "$.content[0]",
     "Next": "NextState"
   }
   ```
5. **Configurar o Bloco 'Pass State':** Configure o Pass State para armazenar o resultado de uma etapa.
   ```json
   {
     "Type": "Pass",
     "InputPath": "$.input_one",
     "ResultPath": "$.result_one",
     "Next": "FinalState"
   }
   ```
6. **Salvar e Executar:** Após todas as configurações, clique em "Salvar" e depois em "Executar". Verifique logs e resultados no console.

**Tecnologias Utilizadas:**
- **AWS Step Functions**
- **IAM** (Gerenciamento de Identidade e Acessos)
- **Lambda** (Exemplo de integração)
