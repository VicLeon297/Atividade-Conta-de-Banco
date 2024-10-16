# Atividade-Conta-de-Banco
Atividade Sistema Fintech

//ALUNO: VICTOR ALFONSO RODRIGUEZ LEON 
//RA:424202742

import java.util.Scanner;

class Conta {
    private double saldo;

    public Conta(double saldoInicial) {
        this.saldo = saldoInicial;
    }

    public void deposito(double valor) {
        if (valor > 0) {
            saldo += valor;
            System.out.println("Depósito realizado com sucesso.");
        } else {
            System.out.println("Valor inválido.");
        }
    }

    public void saque(double valor) {
        if (valor > 0 && valor <= saldo) {
            saldo -= valor;
            System.out.println("Saque realizado com sucesso.");
        } else {
            System.out.println("Saldo insuficiente ou valor inválido.");
        }
    }

    public void transferir(Conta outraConta, double valor) {
        if (valor > 0 && valor <= saldo) {
            saldo -= valor;
            outraConta.deposito(valor);
            System.out.println("Transferência realizada com sucesso.");
        } else {
            System.out.println("Saldo insuficiente para transferência.");
        }
    }

    public double getSaldo() {
        return saldo;
    }
}

class Senha {
    private String senha;

    public Senha(String senhaInicial) {
        this.senha = senhaInicial;
    }

    public boolean autenticar(String senhaEntrada) {
        return this.senha.equals(senhaEntrada);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Inicializando contas e senha
        Conta contaCorrente = new Conta(1000.00);
        Conta poupanca = new Conta(500.00);
        Conta aplicacoes = new Conta(2000.00);
        Senha senha = new Senha("1234");

        while (true) {
            System.out.println("\nMenu de Opções:");
            System.out.println("1 - Depósito Conta Corrente");
            System.out.println("2 - Saque Conta Corrente");
            System.out.println("3 - Saldo Conta Corrente");
            System.out.println("4 - Transferência Conta Corrente -> Poupança");
            System.out.println("5 - Transferência Poupança -> Conta Corrente");
            System.out.println("6 - Transferência Conta Corrente -> Aplicações");
            System.out.println("7 - Transferência Aplicações -> Conta Corrente");
            System.out.println("8 - Saldo Geral (com senha)");
            System.out.println("0 - Sair");

            int opcao = scanner.nextInt();

            switch (opcao) {
                case 1: // Depósito
                    System.out.print("Valor do depósito: ");
                    double valorDeposito = scanner.nextDouble();
                    contaCorrente.deposito(valorDeposito);
                    break;
                case 2: // Saque
                    System.out.print("Valor do saque: ");
                    double valorSaque = scanner.nextDouble();
                    contaCorrente.saque(valorSaque);
                    break;
                case 3: // Saldo
                    System.out.println("Saldo Conta Corrente: " + contaCorrente.getSaldo());
                    break;
                case 4: // Transferência para Poupança
                    System.out.print("Valor da transferência para poupança: ");
                    double valorTransfPoupanca = scanner.nextDouble();
                    contaCorrente.transferir(poupanca, valorTransfPoupanca);
                    break;
                case 5: // Transferência de Poupança para Corrente
                    System.out.print("Valor da transferência para conta corrente: ");
                    double valorTransfCorrente = scanner.nextDouble();
                    poupanca.transferir(contaCorrente, valorTransfCorrente);
                    break;
                case 6: // Transferência para Aplicações
                    System.out.print("Valor da transferência para aplicações: ");
                    double valorTransfAplicacoes = scanner.nextDouble();
                    contaCorrente.transferir(aplicacoes, valorTransfAplicacoes);
                    break;
                case 7: // Transferência de Aplicações para Corrente
                    System.out.print("Valor da transferência para conta corrente: ");
                    double valorTransfAplicParaCorrente = scanner.nextDouble();
                    aplicacoes.transferir(contaCorrente, valorTransfAplicParaCorrente);
                    break;
                case 8: // Saldo Geral
                    System.out.print("Digite a senha: ");
                    String senhaEntrada = scanner.next();
                    if (senha.autenticar(senhaEntrada)) {
                        System.out.println("Saldo Conta Corrente: " + contaCorrente.getSaldo());
                        System.out.println("Saldo Poupança: " + poupanca.getSaldo());
                        System.out.println("Saldo Aplicações: " + aplicacoes.getSaldo());
                    } else {
                        System.out.println("Senha incorreta.");
                    }
                    break;
                case 0: // Sair
                    System.out.println("Saindo...");
                    System.exit(0);
                    break;
                default:
                    System.out.println("Opção inválida.");
            }
        }
    }
}
