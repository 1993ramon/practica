package com.mycompany.practica;


import java.security.SecureRandom;
import java.util.Random;
import java.util.Scanner;

public class Practica {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        SecureRandom random = new SecureRandom();
        int preguntasCorrectas = 0;
        int preguntasIncorrectas = 0;

        System.out.println("Bienvenido al Problema de matematica!");
        System.out.print("Por favor, elige el nivel de dificultad (1-20): ");
        int nivelDificultad = scanner.nextInt();
        System.out.print("Elige el tipo de problema (1: Suma, 2: Resta, 3: Multiplicación, 4: División, 5: Mezcla): ");
        int tipoProblema = scanner.nextInt();

        while (preguntasCorrectas < 10) {
            int num1 = generarNumero(nivelDificultad);
            int num2 = generarNumero(nivelDificultad);
            int respuesta;
            String operador = obtenerOperador(tipoProblema);

            int resultadoEsperado = calcularResultado(num1, num2, operador);

            System.out.print("¿Cuánto es " + num1 + " " + operador + " " + num2 + "? ");
            respuesta = scanner.nextInt();

            if (respuesta == resultadoEsperado) {
                preguntasCorrectas++;
                System.out.println(obtenerRespuestaPositivaAleatoria());
            } else {
                preguntasIncorrectas++;
                System.out.println(obtenerRespuestaNegativaAleatoria());
                System.out.println("Por favor, intenta de nuevo.");
            }
        }

        double porcentajeCorrectas = (double) preguntasCorrectas / 10 * 100;
        if (porcentajeCorrectas >= 75) {
            System.out.println("Felicidades, estás listo para pasar al siguiente nivel!");
        } else {
            System.out.println("Por favor, pide ayuda adicional a tu instructor.");
        }

        scanner.close();
    }

    public static int generarNumero(int nivelDificultad) {
        Random random = new Random();
        int maximo = (int) Math.pow(10, nivelDificultad);
        return random.nextInt(maximo);
    }

    public static String obtenerOperador(int tipoProblema) {
        Random random = new Random();
        switch (tipoProblema) {
            case 1:
                return "+";
            case 2:
                return "-";
            case 3:
                return "*";
            case 4:
                return "/";
            default:
                int operadorAleatorio = random.nextInt(4) + 1;
                return obtenerOperador(operadorAleatorio);
        }
    }

    public static int calcularResultado(int num1, int num2, String operador) {
        int resultado = 0;
        switch (operador) {
            case "+":
                resultado = num1 + num2;
                break;
            case "-":
                resultado = num1 - num2;
                break;
            case "*":
                resultado = num1 * num2;
                break;
            case "/":
                resultado = num1 / num2;
                break;
        }
        return resultado;
    }

    public static String obtenerRespuestaPositivaAleatoria() {
        String[] respuestasPositivas = {"¡Muy bien!", "¡Excelente!", "¡Buen trabajo!", "¡Sigue así!"};
        Random random = new Random();
        int indice = random.nextInt(respuestasPositivas.length);
        return respuestasPositivas[indice];
    }

    public static String obtenerRespuestaNegativaAleatoria() {
        String[] respuestasNegativas = {"No. Por favor intenta de nuevo.", "Incorrecto. Intenta una vez más.",
                "¡No te rindas!", "Sigue intentando."};
        Random random = new Random();
        int indice = random.nextInt(respuestasNegativas.length);
        return respuestasNegativas[indice];
    }
}
