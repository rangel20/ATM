# Challenge requirements

# ATM Challange 💰

The day-to-day life of a developer is full of demands and here will be no different! It's your turn to develop an ATM system! 💰😮 But calm down... before starting, see all the criteria that the system must have to allow the client to:

- To sign in to the system;

- To visualize and manipulate their  bank account information;

- To have access to all transaction made.

⚠️**Remember:** ⚠️the company you represent follows the Test Driven Development (TDD) practice to develop their systems. Check the image below to remember how it works: 👇

![TDDChart](img/tdd_chart.png)

First, we will develop tests, and then the classes of this ATM's system, ok?

The mandatory tests are described below (note that you are free to add more tests), following are the classes the system must have:


## 1. Tests

- `BankTest`: this class contains all the tests related to the methods of our ATM system's `Bank` class.
    - Test Methods:
        - `generateNumberNewAccountTest`: verifies if the method `generateNumberNewAccount` is returning a String 10 digits long, that represents the number of the new account opened.
        - `addPersonCustomerTest`: tests if the method `addPersonCustomer` is adding objects of type `PersonCustomer` the the `peopleCustomers` of the class `Banck`. Represents the insertion of new people customers to the bank, and returns an object of class `PersonCustomer`.
        - `personCustomerLoginTest`: verifies if the method `personCustomerLogin` grants access of people customers and denies accesses with wrong CPF and password combination.
        - `depositTestTransferFundsTestShowBalanceStatementTest`: tests if the method `deposit` is adding to the balance of the bank account the value passed as an argument argumento, and `transferFunds` is transferring amounts in cash between accounts of the same person customer.
        Both the method `deposit` and the method `transferFunds` do not return any value, hence, use the method `showBalanceStatement` to print to the console for us to verify it. With this said, it makes sense that you utilize the three in a single test method because to transfer values from one account to another one, the account that will cede the money must have a positive balance.
        - `depositTestWithdrawTestShowBalanceStatementTest`: test if the method `deposit` is adding to the balance of the bank account the value passed as an argument, and the method `withdraw` is subtracting from the balance of the bank account the correct amount passed as an argument. As the method `deposit` and the method `withdraw` do not return values, you must use the method `showBalanceStatement` to print the console and verify it. With that, it makes sense to test the three in a single test method because to be able to withdraw values from one account, it must have a positive balance.

- `AccountTest`: this class contains tests related to the methods from the `Account` class.
    - Test Methods:
        - `constructorTest`: evaluates if the constructor is initializing the `Account` class attributes correctly.
        - `addTransactionTestReturnBalanceTest`: verifies if the method `addTransaction` is adding a transaction to the account history performed by the given method realizada, and analyses if the method `returnBalance` retunrs the account balance correctly. It makes sense to test both together, as the method `addTransaction` does not have a return, we use `returnBalance` to verify if the transaction was correctly added to the account and if the balance is being returned without errors. 
        - `returnAccountSummaryTest`: verifiesif the method `returnAccountSummary` is presenting a summary of the bank account.
        - `returnBalanceStatementTest`: tests if the method `returnBalanceStatement` is presenting the balance statementof the bank account.
        - `getAccountIdTest`: evaluates if the method `Getter` of the attribute `accountId` is returning the identification number of the account.
        - `getPersonCustomerTest`: verifies if the method `Getter` of the attribute `personCustomer` is returning the person customer of the bank account.

- `PersonCustomerTest`: this class haas the test methods of `PersonCustomer` class.
    - Test Methods:
        - `constructorTest`: evaluates if the class's constructor is initializing its attribute correctly and printing a message to the console indicating that an object of the `PersonCustomer` class has been instantiated.
        - `addAccountTestReturnNumberOfAccountsTest`: verifies if the method `addAccount` is adding a new account to the person customer, as well as analyzing if the method `returnNumberOfAccounts` returns the number that represents the number of accounts that a person customer owns.
        It makes sense to test these two methods together because the method `addAccount` has no return, then we use the method `returnNumberOfAccount` to verify if a given account was added and we leverage the moment to test its operation. 
        - `returnSpecificAccountBalanceTest`: tests if the method `returnSpecificAccountBalance` returns the correct balance of a specific bank account.
        - `returnSpecificAccountIdBalanceTest`: verifies if the method `returnSpecificAccountIdBalance` is returning the correct identification number of a specific bank account.
        - `returnAccountStatementTest`: evaluates if the method `returnSpecificAccountStatement` returns the bank statement of a specific person customer's account.
        - `addSpecificAccountTransactionTest`: tests if the method `addSpecificAccountTransaction` is adding a transaction to a specific person customer's account.
        - `validatePasswordTest`: tests if the method `validatePassword` is verifying if the password passed by parameter is the same as the one registered when the person customer was created in the system.
        - `returnAccountsSummaryTest`: analyze if the method `returnAccountsSummary` returns a summary of the person customer's accounts.
        - `getCpfTest`: evaluates if the method `Getter` of the attribute `cpf` of the person customer is returning the registered CPF.

- `TransactionTest`: this class contains all the tests related to the class `Transaction`.
    - Test Methods:
        - `constructorTest`: verifies if the constructor method is initializing the attributes correctly.
        - `getAmountTest`: test if the method `Getter` of the amount attribute is returning the amount correctly.
        - `returnTransactionSummaryTest`: evaluates if the method `returnTransactionSummary` presents the transaction summary correctly.
        - `returnInstantTest`: verifies if the method `returnInstant` returns the correct moment when the transaction occurred, with date, time, minute, and second.

Ufs! So many tests, huh? 😅 

Now let's go to the classes that the ATM system must have!

![MapaGeral](img/general_conceptual_map.png)

## 2. Classes

- `Bank`: represents the bank entity of our ATM. This class is responsible for creating new people customers in the bank, and also verifies and validates the person customer login at the ATM.
    - Attributes:
        - `peopleCustomers`: this attribute is an array of objects of the class `PersonCustomer` (e.g. ArrayList<PersonCustomer>), and represents the list of people customers who have open bank accounts (a person customer can have more than one open account).
        - `accounts`: this attribute is an array of objects of the class `AccountsC` (e.g. ArrayList<Account>) and represents the list of open bank accounts, where each one belongs to a person customer. The accounts are identifies by a 10-digit String, that represents the unique identification number generated by the method `generateNewAccountNumber` of the class `Bank`.
    
    - Methods:
        - `generateNewAccountNumber`: this method is public, must return a String, and does not receive any argument. It is responsible for generating and returning a 10-digit String, that represents the unique identification number of an account, in other words, for each new account opened, it must generate a unique number (e.g. "8514540006").         
        - `addPersonCustomer`: this method is public, returns an object of type `PersonCustomer`, and must receive 3 arguments of type String (name, cpf, and password). This method must instantiate an object of the class `PersonCustomer` and add it to the array `peopleCustomers`, and must return that created object of the class `PersonCustomer`.
        - `addAccount`: this method is public and returns the type `void`, that is, it does not return any value, and receives 1 argument (newAccount) of type `Account`. This method is responsible for receiving an account as a parameter and adding to the array `accounts`.
        - `personCustomerLogin`: this method is public, returns an object of type `PersonCustomer`, and receives 2 arguments of type String (cpf and password). It is responsible for searching on the array `peopleCustomers`, the object owner of the cpf passed by parameter, and verifies if the password is correct. In case the cpf and the password belong to any object that is in the array `peopleCustomers`, the object that represent the person customer must be returned; otherwise, this method must return `null`.
        - `transferFunds`: this method is public, must have the return type `void` (does not return any value), and must receive four attributes, which are `personCustomer`, of the class type `PersonCustomer`(representing the person customer logged in); `fromAccount`, of type integer that represents the index of the array `accounts` of the account (responsible for assigning the money for the transfer); `toAccount`, of type integer that represents the index of the array `accounts` (to the account that will receive the transfer); and finally, `amount`, of type `double` (representing the value that will be transferred ). 
        - `withdraw`: this method is public, must have the return type of `void` (does not return any value), and must receive three attributes, which are `peopleCustomers`, of the class type `PersonCustomer` (representing the person customer logged in); `fromAccount`, of type integer (representing the index of the array `accounts` of the account in which the money will be withdrawn); and finally, `amount`, of type `double` (represents the value that will be withdrawn).
        - `deposit`: this method is public, must have the return type of `void` (does not return any value), and must receive three attributes, which are `peopleCustomers`, of the class type `PersonCustomer` (representing the person customer logged in); `toAccount`, of type integer (represents the index of the array `account` of the account where the money will be deposited); and finally, `amount`, of type `double` (representing the value that will be deposited).
        - `showBalanceStatement`: this method is also public, must have the return of type `void`, and must receive two attributes, which are peopleCustomer, of the class type `PersonCustomer` (representing the person customer owner of the account), and `account`, of type integer (represents the index of the account in the array `accounts` that will have the balance statement shown).

**Check out this tip:** 👀 in the method `generateNumberNewAccount`, use the method `nextInt`, of the class `Random` from the package `java.util`, to generate the digits. Generate a digit at a time and concatenate in a String. Finally, check if some account object already created has the same identification number. If it has, repeat the process again until it generates a unique identification number. And in the method `transferFunds` take into account that a person customer can only transfer money between their own account, a checking account, and a savings account. 

- `Account`: represents the bank accounts, where we have transaction-related methods, and shows balance information.
    - Attributes:
        - `accountType`: An attribute of type String that indicates if the account is "Savings" or "Checking".
        - `accountId`: An attribute of type String that represents the unique identification number of a bank account.
        - `personCustomer`: An attribute of type `PersonCustomer`, representing the person customer owner of the given account.
        - `transactions`: This attribute is an array of objects of the class `Transaction` (ex: ArrayList<Transaction>), responsible for storing all the transactions made on the account.

    - Methods:
        - Constructor: This constructor method must receive as arguments `accountType` of type String; `personCustomer` of the class type `PersonCustomer`; and `bank` of the class type `Bank`. It must use these arguments to initialize the respective attributes and use the method `generateNumberNewAccount` to generate the unique identification number to the account.
        - `addTransaction`: This method is public and has the return type `void`. Must receive two arguments, which are `amount` of type `double` and the `description` of type String. `amount` indicates the value that involves the transaction, and `description` indicates what sort of transaction was performed (e.g. Deposit received, Withdrawal made, etc.). Must use these values to instantiate an object of the class `Transaction`, passing amount and the description (ex: `Transaction newTransaction = new Transaction(amount, "Transfer received");`) and add this new object to the array `transactions`.
        - `returnBalance`: This method is public and returns a type `double`. It uses the array `transactions` to calculate the given account balance. 
        - `returnAccountSummary`: is public and returns a String with the account summary, unique identification number, balance, and account type (Savings or Checking). It uses the method `returnBalanceStatement` to calculate the account balance.
        - `returnBalanceStatement`: This method is public and has a return type of `void`. This method prints to the console all the account transactions (one per line). In other words, this method loops through the array `transactions` and for each object in the array, it calls the method `returnTransactionSummary` of the class `Transaction`.
        - `getAccountId`: `Getter` method of the attribute `accountId`.
        - `getPersonCustomer`: `Getter` method of the attribute `personCustomer`.
        
⚠**Attention:** note that the sum of transactions indicates the account balance, where withdrawals and transfers sent are negative values and deposits and transfers received are positive values in this sum.

- `PersonCustomer`: this class represents bank customer people.
    - Attributes:
        - `fullName`: Attribute of type String to store the person customer's name.
        - `cpf`: Attribute of type String to store the person customer's CPF.
        - `password`: Attribute of type String to store the person customer's password.
        - `accounts`: This attribute is an array of objects of the class `Account` (ex: ArrayList<Account>), responsible for storing all the accounts the person customer owns.

    - Method:
        - Constructor: initializes the attributes of the class `PersonCustomer` and receives three attributes of type String, which are `name`, `cpf`, and `password`. These arguments are used to initialize the respective attribute. Finally, this constructor method prints a message to the console indicating that the person customer was created (e.g. "New person customer Alexiania Silva with CPF: 433.892.200-11 created!")
        - `addAccount`: this method is public and must return type `void`. It receives an argument `account`, of the type of the class `Account`, and adds it to the array `accounts`.
        - `returnNumberOfAccounts`: public method that returns an integer (it does not receive any argument). The integer number returned by this method is the number of objects in the array `accounts`, that is, its size.
        - `returnSpecificAccountBalance`: this method is public and returns a value of type `double`, receiving as an argument an `index` of type integer (to be used as an index of the array `accounts`) and using the method `returnBalance` of the class `Account` to return the balance.
        - `retornarIdContaEspecifica`: esse método é público e retorna um valor do tipo String, recebendo um argumento `indice` do tipo inteiro (para ser usado como índice no array `contas`) e usando o método `getIdConta` da classe `Conta` para retornar o número identificador único da conta.
        - `retornarExtratoContaEspecifica`: esse método é público e tem um retorno do tipo `void`, recebendo um argumento `indice` do tipo inteiro (para ser usado como índice no array `contas`) e usando o método `retornarExtrato` da classe `Conta` para imprimir todas as transações de uma determinada conta.
        - `adicionarTransacaoContaEspecifica`: esse método público e tem retorno do tipo `void`, recebendo 3 argumentos, que são `indice` do tipo inteiro, `quantia` do tipo `double` e `descricao` do tipo String. Esse método utiliza o argumento `indice` para selecionar uma conta específica dentro do array `contas` e chama o método `adicionarTransacao` da classe `Conta` para adicionar uma transação e passar os argumentos `quantia` e `descricao`.
        - `validarSenha`: esse método é público e retorna um valor `boolean`, recebendo um argumento `senha` do tipo String e verificando se essa String é igual ao atributo `senha` do objeto. Se for, retorna `true`, se não for retorna `false`.
        - `retornarResumoContas`: esse método é público e tem retorno do tipo `void`. Ele não recebe argumento e percorre o array `contas`, utilizando o método `retornarResumoConta` da classe `Conta` para imprimir o resumo da conta.
        - `getCpf`: método `Getter` do atributo `cpf`.

- `Transacao`: essa classe é utilizada para representar a transação nas contas do banco.
    - Atributos:
        - `quantia`: esse atributo é do tipo `double` e representa o valor da transação.
        - `instante`: esse atributo é do tipo String e armazena a data e a hora que a transação ocorreu.
        - `descricao`: esse atributo é do tipo String e armazena a descrição da transação.
        - `conta`: esse atributo é do tipo `Conta` e armazena o objeto `conta` da transação.
    
    - Métodos:
        - Construtor: esse método recebe dois argumentos, que são `quantia` do tipo `double` e `descricao` do tipo String. Ele usa esses argumentos para inicializar seus respectivos atributos e chama o método `retornarInstante` para armazenar a data e a hora que essa transação foi realizada.
        - `getQuantia`: método `Getter` do atributo `quantia`.
        - `retornarResumoTransacao`: esse método é público e retorna uma String que representa o resumo da transação, contendo as informações instante, quantia e descrição. Ele não recebe nenhum argumento.
        - `retornarInstante`: esse método é público e retorna um String que representa o instante em que esse método é invocado. Ele usa a classe `LocalDateTime` para recuperar o momento em que o método é invocado (`LocalDateTime.now()`) e a classe `DateTimeFormatter` para formatar para o padrão brasileiro (ex: 20/01/2022 10:24:30). Esse método é usado no método construtor para inicializar o atributo `instante`.

![MapaMental](img/mapa_mental_classes.png)

Para ajudar, implemente agora a classe `CaixaEletronico`, que contém o método `main`. Dessa forma, você terá um ponto de partida. Agora siga o passo a passo abaixo: 👇

1. Primeiro importe a classe `Scanner`, e então escreva o método `main`. Aqui você deve instanciar um objeto da classe `Banco` e usá-la para criar três pessoas clientes e duas contas para cada pessoa cliente.

⚠**Atenção⚠:** Após a criação das pessoas clientes e suas respectivas contas bancárias, você vai entrar em um laço infinito que é o sistema do caixa eletrônico em si. A princípio ele mostra uma mensagem de boas-vindas e permite que a pessoa cliente possa entrar com seus dados para poder acessar sua conta. Se a pessoa cliente entrar com os dados incorretos, o fluxo do programa vai entrar na primeira condição (`if`) e reapresentará a mensagem de boas-vindas e os campos para que a pessoa cliente possa tentar novamente. Quando a pessoa cliente entra com os dados corretos,  o fluxo do sistema entra na segunda condição (`else`) e é apresentado um menu para manipulação das suas contas bancárias.


2. Na segunda etapa você verá um resumo das contas bancárias da pessoa usuária e também um menu com cinco opções (quatro delas para manipular a sua conta bancária e a quinta para fazer o logout do sistema e voltar para a tela de boas-vindas com os campos para fazer o login). 

👀Observe que cada opção é uma condição `if`/`else`! Dentro delas fazemos os tratamentos de dados inseridos de forma errada, com mensagens que indiquem o que foi que a pessoa cliente errou. Já quando os dados são inseridos corretamente, chamamos os respectivos métodos do banco para realizar a operação relativa à opção selecionada.

```java
package com.trybe.caixaeletronico;

import java.util.Scanner;

public class CaixaEletronico {

  public static void main(String[] args) {

	  Scanner sc = new Scanner(System.in);
	
    Banco banco = new Banco();
    
    /* adiciona algumas pessoas clientes ao banco criando ja uma conta poupanca 
     * e em seguida adiciona uma conta corrente para essas pessoas
     */
    
    // pessoa cliente 1
    PessoaCliente pessoaCliente1 = banco.adicionarPessoaCliente("Alexiania Pereira", "842.074.410-77", "1234"); 
    banco.adicionarConta("Poupança", pessoaCliente1);
    banco.adicionarConta("Corrente", pessoaCliente1);
    
    // pessoa cliente 2
    PessoaCliente pessoaCliente2 = banco.adicionarPessoaCliente("Abadiania Silva", "848.725.510-87", "1234");
    banco.adicionarConta("Poupança", pessoaCliente2);
    banco.adicionarConta("Corrente", pessoaCliente2);

    // pessoa cliente 3
    PessoaCliente pessoaCliente3 = banco.adicionarPessoaCliente("Camaragibe Oliveira", "433.892.200-11", "1234");
    banco.adicionarConta("Poupança", pessoaCliente3);
    banco.adicionarConta("Corrente", pessoaCliente3);
    // laco infinito
    while (true) {
      
      System.out.println("\n\nBem-vindo ao Banco da Trybe\n\n");
      System.out.print("Entre com seu CPF: ");
      String pessoaClienteCpf = sc.nextLine();
      System.out.print("Entre com sua senha: ");
      String senha = sc.nextLine();

      PessoaCliente pessoaClienteAutenticada = banco.pessoaClienteLogin(pessoaClienteCpf, senha);
      
      if (pessoaClienteAutenticada == null) {
        System.out.println("Combinação de CPF e senha incorretos. Tente novamente");

      } else {

        int op;

        // menu para manipulacao das contas da pessoa cliente
        do {
          
          // mostra o resumo das contas da pessoa cliente
      	  pessoaClienteAutenticada.retornarResumoContas();

          System.out.println("O que você gostaria de fazer?");
          System.out.println("  1) Mostrar Extrato");
          System.out.println("  2) Sacar");
          System.out.println("  3) Depositar");
          System.out.println("  4) Transferir");
          System.out.println("  5) Sair");
          System.out.println();
          System.out.print("Entre com sua opção: ");

          op = sc.nextInt();

          if (op < 1 || op > 5) {
            System.out.println("Opção inválida, escolha uma opção válida.");
          }
          
          // processando a escolha
          if (op == 1) {
            
            int conta;

            // pega o indice da conta para imprimir o extrato
            do {
              System.out.printf("Entre com o número (1-%d) para a conta\nque "
                                       + "o extrato será impresso: ", pessoaClienteAutenticada.retornaNumeroDeContas());
              conta = sc.nextInt() - 1;
              if (conta < 0 || conta >= pessoaClienteAutenticada.retornaNumeroDeContas()) {
                System.out.println("Número inválido, tente novamente.");
              }else {
            	break;
              }
            } while (true);
        	
        	 banco.mostrarExtrato(pessoaClienteAutenticada, conta);
            
            
            
            
          } else if (op == 2) {
        	
        	int deConta;
            double quantia;
            double saldoConta;

            // pega o indice da conta para saque
            do {
              System.out.printf("Entre o número (1-%d) para selecionar a conta para "
                                   + "o saque: ", pessoaClienteAutenticada.retornaNumeroDeContas());
              deConta = sc.nextInt() - 1;
              if (deConta < 0 || deConta >= pessoaClienteAutenticada.retornaNumeroDeContas()) {
                System.out.println("Índice de conta inválido, tente novamente.");
              } else {
            	break;
              }
            } while (true);
            
            // retorna o saldo da conta selecionada para ver se tem fundos suficientes
            saldoConta = pessoaClienteAutenticada.retornarSaldoContaEspecifica(deConta);

            // pega a quantia para o saque
            do {
              System.out.printf("Entre com a quantia a ser sacada (máximo R$%.02f): R$ ", saldoConta);
              quantia = sc.nextDouble();
              if (quantia < 0) {
                System.out.println("quantia deve ser maior que zero.");
              } else if (quantia > saldoConta) {
                System.out.printf("quantia não pode ser maior que o saldo "
                                        + "de R$ %.02f.\n", saldoConta);
              } else {
            	break;
              }
            } while (true);

        	banco.sacar(pessoaClienteAutenticada, deConta, quantia);
            
          } else if (op == 3) {
        	
        	int paraConta;
            double quantia;

            // pega o indice da conta para deposito
            do {
              System.out.printf("Entre com o número (1-%d) para selecionar a conta para "
                                     + "depósito: ", pessoaClienteAutenticada.retornaNumeroDeContas());
              paraConta = sc.nextInt() - 1;
              
              if (paraConta < 0 || paraConta >= pessoaClienteAutenticada.retornaNumeroDeContas()) {
                System.out.println("Índice de conta inválido, tente novamente.");
              
              } else {
            	break;
              }
            } while (true);

            // pega quantia para depositar
            do {
              System.out.printf("Entre com a quantia de depósito: R$ ");
              quantia = sc.nextDouble();
              
              if (quantia < 0) {
                System.out.println("quantia deve ser maior que zero.");
              
              } else {
            	break;
              }
            } while (true);

        	// realiza o deposito
            banco.depositar(pessoaClienteAutenticada, paraConta, quantia);
            
          } else if (op == 4) {
        	
        	int daConta;
        	int paraConta;
        	double quantia;
        	double saldoConta;
        	
            // pega o indice de uma conta retirar o valor da transferencia
            do {
              System.out.printf("Entre o número (1-%d) para "
            	                      + "retirar o valor para transferência: ", pessoaClienteAutenticada.retornaNumeroDeContas());
              daConta = sc.nextInt() - 1;
              if (daConta < 0 || daConta >= pessoaClienteAutenticada.retornaNumeroDeContas()) {
                System.out.println("Índice de conta inválido, tente novamente.");
              } else {
            	break;
              }
            } while (true);

            // retorna o saldo da conta selecionada para ver se tem fundos suficientes
            saldoConta = pessoaClienteAutenticada.retornarSaldoContaEspecifica(daConta);

            // pega o indice da conta que vai receber o valor da transferencia
            do {
              System.out.printf("Entre o número (1-%d) para "
                                     + "selecionar a conta que receberá a transferência: ", pessoaClienteAutenticada.retornaNumeroDeContas());
              paraConta = sc.nextInt() - 1;
              if (paraConta < 0 || paraConta >= pessoaClienteAutenticada.retornaNumeroDeContas()) {
                System.out.println("Índice de conta inválido, tente novamente.");
              } else {
            	break;
              }
            } while (true);

            // pega o valor para transferir
            do {
              /* pega a quantia para ser transferida de uma conta da pessoa cliente para outra
               * levando em consideracao o saldo da conta que cedera o dinheiro
               */
              System.out.printf("Entre com a quantia para ser transferida (máximo R$%.02f): R$ ", saldoConta);
              quantia = sc.nextDouble();
              
              if (quantia < 0) {
                System.out.println("quantia deve ser maior que zero.");
              
              } else if (quantia > saldoConta) {
                System.out.printf("quantia não pode ser maior que o valor do saldo "
                                       + "de R$.02f.\n", saldoConta);
              } else {
            	break;
              }
            } while (true);
            
            // envia as informacoes para o banco realizar a trasnferencia
            banco.transferirFundos(pessoaClienteAutenticada, daConta, paraConta, quantia);
            
          } else if (op == 5) {
        	System.out.println("Logout realizado com sucesso!");
            break;
          }

        } while (true);    	
    	
      }// fim else
      
      
    }// fim loop infinito
  } 
}
```
⚠**Atenção⚠:** essa classe `CaixaEletronico` é a principal do nosso sistema, pois ela contém o método `main` e como podemos ver na implementação, ele é o responsável por toda a interação com a pessoa cliente. Em outras palavras, essa classe é a interface entre a pessoa cliente e nosso sistema do banco. Com ela e as informações descritas anteriormente sobre as classes e seus métodos, você conseguirá entregar essa demanda com sucesso! 🚀 

#VQV

## Exemplo

Considerando que tenha executado exatamente o código da classe `main` acima e interagido como se fôssemos a pessoa cliente Camaragibe Oliveira, teríamos a seguinte interação com o console:
```
Nova pessoa cliente Alexiania Pereira com CPF: 842.074.410-77 criada!

Nova pessoa cliente Abadiania Silva com CPF: 848.725.510-87 criada!

Nova pessoa cliente Camaragibe Oliveira com CPF: 433.892.200-11 criada!



Bem-vindo ao Banco da Trybe


Entre com seu CPF: 433.892.200-11
Entre com sua senha: 1234


Resumo das Contas da pessoa Camaragibe Oliveira:

1) 1376245820 : R$0.00 : Poupança

2) 1400842111 : R$0.00 : Corrente


O que você gostaria de fazer?
  1) Mostrar Extrato
  2) Sacar
  3) Depositar
  4) Transferir
  5) Sair

Entre com sua opção: 3
Entre com o número (1-2) para selecionar a conta para depósito: 1
Entre com a quantia de depósito: R$ 2000


Resumo das Contas da pessoa Camaragibe Oliveira:

1) 1376245820 : R$2000.00 : Poupança

2) 1400842111 : R$0.00 : Corrente


O que você gostaria de fazer?
  1) Mostrar Extrato
  2) Sacar
  3) Depositar
  4) Transferir
  5) Sair

Entre com sua opção: 3
Entre com o número (1-2) para selecionar a conta para depósito: 2
Entre com a quantia de depósito: R$ 4000


Resumo das Contas da pessoa Camaragibe Oliveira:

1) 1376245820 : R$2000.00 : Poupança

2) 1400842111 : R$4000.00 : Corrente


O que você gostaria de fazer?
  1) Mostrar Extrato
  2) Sacar
  3) Depositar
  4) Transferir
  5) Sair

Entre com sua opção: 4
Entre o número (1-2) para retirar o valor para transferência: 2
Entre o número (1-2) para selecionar a conta que receberá a transferência: 1
Entre com a quantia para ser transferida (máximo R$4000.00): R$ 2000


Resumo das Contas da pessoa Camaragibe Oliveira:

1) 1376245820 : R$4000.00 : Poupança

2) 1400842111 : R$2000.00 : Corrente


O que você gostaria de fazer?
  1) Mostrar Extrato
  2) Sacar
  3) Depositar
  4) Transferir
  5) Sair

Entre com sua opção: 1
Entre com o número (1-2) para a conta
que o extrato será impresso: 1

Extrato da conta 1376245820

21/01/2022 14:21:52 -------- Transferência recebida: R$ 2000.00 +
21/01/2022 14:21:32 -------- Depósito recebido: R$ 2000.00 +



Resumo das Contas da pessoa Camaragibe Oliveira:

1) 1376245820 : R$4000.00 : Poupança

2) 1400842111 : R$2000.00 : Corrente


O que você gostaria de fazer?
  1) Mostrar Extrato
  2) Sacar
  3) Depositar
  4) Transferir
  5) Sair

Entre com sua opção: 
```

Muito legal né? Bom trabalho! 🚀 #VQV
---