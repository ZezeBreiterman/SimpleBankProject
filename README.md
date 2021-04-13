# SimpleBankProject
Aplicación en la cual se crea un usuario con su ID de cuenta y tiene la capacidad de ver el saldo, retirar e ingresar dinero, ver saldo anterior y calcular un plazo fijo

// =========================================Se ejecuta en el Main=========================================

package com.company;

import java.util.Scanner;

public class Cuenta {

    String nombre;
    String idCuenta;
    int saldo = 0;
    int saldoAnterior;
    Scanner sc = new Scanner(System.in);


    private int getSaldo() {
        return saldo;
    }

    public int getSaldoAnterior() {
        return saldoAnterior;
    }

    protected Cuenta(String nombre, String idCuenta) {
        this.nombre = nombre;
        this.idCuenta = idCuenta;
    }
    void depositar (int cantidad){
        if (cantidad > 0) {
            saldoAnterior = saldo;
            saldo += cantidad;
        }
    }
    void retirar (int cantidad){
        if (cantidad > 0 && (saldo-cantidad > 0)) {
            saldoAnterior = saldo;
            saldo -= cantidad;
        }
    }

    void calcularInteres () {
        double porcentajeInteres = 1.5;
        int cantidad;
        int años;
        do {
            System.out.println("Que cantidad de Dinero quiere depositar a largo plazo? ");
            cantidad = sc.nextInt();
            System.out.println("Cuantos años quiere depositar a largo plazo? ");
            años = sc.nextInt();
            if (cantidad > saldo){
                System.out.println("No posee suficientes fondos");
            }if (cantidad<0 && años < 0) {
                System.out.println("La cantidad de años y dinero debe ser superior a 0");
            }
        }while(cantidad<0 && años < 0 && cantidad > saldo);
        System.out.println("En " + años + " años, con una taza de interes de " + porcentajeInteres + "% " + ", usted recibiria: " + (cantidad * años * porcentajeInteres) );

    }

    void mostrarMenu (){
        char opcion = '\0';
        System.out.println();
        System.out.println("Bienvenido " + nombre + "!");
        System.out.println("Su ID es: " + idCuenta );
        System.out.println();
        System.out.println("Que desea hacer?");

        System.out.println("A. Ver Saldo");
        System.out.println("B. Hacer un deposito");
        System.out.println("C. Retirar dinero");
        System.out.println("D. Ver saldo anterior");
        System.out.println("E. Calcular interes");
        System.out.println("S. Salir");
        do {
            System.out.println("====================================================");
            System.out.println("Eliga su opcion");
            opcion = sc.next().charAt(0);
            opcion = Character.toUpperCase(opcion);
            switch (opcion){
                case 'A':
                    System.out.println("Su saldo es de "+getSaldo() + " $");

                    break;
                case 'B':
                    System.out.println("Cuanto desea depositar? ");
                    depositar( sc.nextInt());
                    System.out.println("Su nuevo saldo es de " +getSaldo() + " $");

                    break;
                case 'C':
                    System.out.println("Cuanto desea retirar? ");
                    retirar( sc.nextInt());
                    System.out.println("Su nuevo saldo es de "+getSaldo() + " $");

                    break;
                case 'D':
                    System.out.println("su saldo anterior es de : " + getSaldoAnterior());

                    break;
                case 'E':
                    calcularInteres();
                    break;
            }
        }while (opcion != 'S');

    }
