# ==================================================
# JUEGO PIEDRA, PAPEL O TIJERA
# Basado en Diagrama de Casos de Uso
# Funcionalidades: Iniciar juego, Elegir opción, Consultar marcador
# ==================================================
# ----------------------
# IMPORTACIÓN Y VARIABLES GLOBALES
# ----------------------
import random  # Para generar jugada aleatoria de la computadora
# Variables y tipos de datos
puntos_usuario = 0          # Tipo entero: puntos del jugador
puntos_pc = 0               # Tipo entero: puntos de la computadora
opciones = ["piedra", "papel", "tijera"]  # Tipo lista: jugadas permitidas
jugar = True                # Tipo booleano: controla el ciclo del juego
# ==================================================
# CASO DE USO 1: INICIAR JUEGO
# ==================================================
def iniciar_juego():
     """Función que da inicio al juego y muestra el menú principal"""
     print("\n=====================================")
     print("      PIEDRA, PAPEL O TIJERA")
     print("=====================================")
     print("1. Jugar nueva ronda")
     print("2. Consultar marcador")
     print("3. Salir del juego")
     print("-------------------------------------")
# ==================================================
# CASO DE USO 2: ELEGIR OPCIÓN
# ==================================================
def elegir_opcion():
     """Permite al usuario seleccionar su jugada y valida el dato ingresado"""
     while True:
         try:
             seleccion = int(input("\nElige tu jugada: \n1 = Piedra \n2 = Papel \n3 = Tijera \nIngresa número: "))
            
             # Condicional para verificar que la opción sea válida
             if seleccion >= 1 and seleccion <= 3:
                 return opciones[seleccion - 1]
             else:
                 print("❌ Error: Ingresa solo 1, 2 o 3.")
        
         except ValueError:
             print("❌ Error: Debes escribir un número válido.")
def generar_jugada_pc():
     """Genera la elección aleatoria de la computadora"""
     return random.choice(opciones)
def comparar_y_definir_ganador(usuario, computadora):
     """Compara ambas jugadas, determina el resultado y actualiza puntuación"""
     global puntos_usuario, puntos_pc  # Accedemos a las variables globales
     print(f"\nTu jugada: {usuario.upper()}")
     print(f"Jugada PC: {computadora.upper()}")
     # Condicionales para evaluar todas las posibilidades
     if usuario == computadora:
         print("⚖️ Resultado: EMPATE - No se suman puntos")
    
     elif (usuario == "piedra" and computadora == "tijera") or \
          (usuario == "papel" and computadora == "piedra") or \
          (usuario == "tijera" and computadora == "papel"):
         print("🏆 ¡GANASTE!")
         puntos_usuario = puntos_usuario + 1  # Operador aritmético
    
     else:
         print("💻 Gana la computadora")
         puntos_pc += 1  # Operador de suma abreviado
# ==================================================
# CASO DE USO 3: CONSULTAR MARCADOR
# ==================================================
def consultar_marcador():
     """Muestra la puntuación acumulada hasta el momento"""
     print("\n=====================================")
     print("📊 MARCADOR ACTUAL")
     print(f"Tú: {puntos_usuario} puntos")
     print(f"Computadora: {puntos_pc} puntos")
     print("=====================================")
# ==================================================
# FLUJO PRINCIPAL DEL PROGRAMA
# ==================================================
while jugar:  # Bucle principal del juego
     iniciar_juego()
    
     try:
         opcion_menu = int(input("Selecciona una opción del menú: "))
         if opcion_menu == 1:
             # Ejecución completa de una ronda
             jugada_usuario = elegir_opcion()
             jugada_computadora = generar_jugada_pc()
             comparar_y_definir_ganador(jugada_usuario, jugada_computadora)
        
         elif opcion_menu == 2:
             consultar_marcador()
        
         elif opcion_menu == 3:
             print("\n👋 Juego finalizado. ¡Hasta la próxima!")
             jugar = False  # Finaliza el bucle
        
         else:
             print("⚠️ Opción no válida, intenta nuevamente.")
    
     except ValueError:
         print("⚠️ Ingresa un número válido para elegir en el menú.") 
