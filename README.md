# Prova Ab2 teórica P3
## Diagrama de interfaces/classes
![foto](https://i.imgur.com/Q54JNMl.png)
## Padrões utilizados:
- Strategy
    - Utilizado para o controle de funcionamento do pagamento para os diferentes tipos de empregado.
    
- Command
    - Utilizado para implementar o funcionamento do undo/redo.
    
## Detalhamento

### Interfaces implementadas:
- TipoEmpregado
    - O funcionamento de diferentes tipos de empregados ficam a cargo dessa interface, implementada inspirada no padrão de design Strategy, um objeto do tipo Empregado tem como um dos seus atributos uma referência à uma instância de uma classe que implemente esta interface. Desta forma, a alteração do tipo de empregado fica fácil, já que só é necessário que se passe a instância referente ao tipo desejado.
    
- AddPayData
    - Uma interface feita para auxiliar a funcionalidade de TipoEmpregado. Como diferentes tipos de empregados necessitam diferentes formas de processar seu trabalho, (Cartão de ponto, resultado de venda), diferentes estruturas são necessárias para armazenar isto. Ademais, para manter a interface de TipoEmpregado intacta, implementamos esta interface para que em vez dos parâmetros referentes ao tipo de dado fossem passados, um objeto do tipo AddPayData o seja. 
    
- MetodoPagamento
    - Esta interface é utilizada para determinar o processamento do método de pagamento ao funcionário(Banco, correio, cheque). Desta forma, o sistema é capaz de trocar entre métodos de pagamento facilmente, dado que só é necessário trocar a instância de MetodoPagamento utilizada.
    
- Command
    - Esta interface é a utilizada para implementar o segundo padrão de design, que tem o mesmo nome. A interface gráfica do sistema irá, ao receber um comando, procurar o objeto certo para executar a requisição do usuário, esta, retornará uma instância de Command, que contem a lógica necessária tanto para executar quando para desfazer o comando enviado pelo usuário. Duas pilha destas instâncias são usadas, então, para manter o histórico de ações do programa. Quando a função undo é solicitada, um pop() é feito no atributo Comandos, e então, a função undo() da instância de Command recebida é executada. Logo em seguida, um push() dessa instância é feita desta vez a ComandosRedo, e quando um eventual redo() é solicitado, o processo inverso ocorre, sendo que desta vez, a função execute() da instância é executada, implementando assim, por completo, a funcionalidade undo/redo.
    

### Classes base definidas:
- Empregado
    - classe utilizada para armanezar e organizar as funcionalidades requeridas para a manutenção de um funcionário, contém referências para as instâncias dos objetos que implementam as interfaces acima mencionadas, compondo e modularizando o funcionamento do mesmo.
    
- FolhaDePagamento
    - Contém referências a uma lista dos empregados, e as pilhas de histórico dos comando executados.
    - Os métodos definidos para esta classe implementam o resto das funcionalidades requeridas do produto, utilizando-se também de métodos capazes de gerar objetos do tipo Command, logo incluindo-se no processo de armazenamento das ações executadas pelo usuário.
- GUI
    - Interface gráfica responsável por receber e interpretar as requisições do usuário, adicionando corretamente ao histórico de ações os objetos Command gerados pelas requisições feitas pelo usuário.
 
- SindicatoMembro
    - Uma classe auxiliar a Empregado, utilizada para guardar e manter os atributos e métodos relacionados especificamente a operações do Sindicato.
    
