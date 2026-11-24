# cine_asientos.py

def crear_sala(filas, columnas):
    return [["L"] * columnas for _ in range(filas)]


def mostrar_sala(sala):
    print("\n--- PANTALLA ---")
    for i, fila in enumerate(sala, 1):
        print(f"F{i}:", " ".join(fila))


def pedir_asiento(sala):
    f_max, c_max = len(sala), len(sala[0])
    while True:
        try:
            f, c = int(input(f"Fila (1-{f_max}): ")), int(input(f"Columna (1-{c_max}): "))
            if 1 <= f <= f_max and 1 <= c <= c_max:
                return f - 1, c - 1
            print("Asiento fuera de rango.")
        except ValueError:
            print("Solo números enteros.")


def cambiar_estado(sala, actual, nuevo, msg_ok, msg_no):
    f, c = pedir_asiento(sala)
    if sala[f][c] == actual:
        sala[f][c] = nuevo
        print(msg_ok)
    else:
        print(msg_no)


def estadisticas(sala):
    libres = sum(fila.count("L") for fila in sala)
    ocupados = sum(fila.count("X") for fila in sala)
    print(f"Libres: {libres} | Ocupados: {ocupados}")


def menu():
    while True:
        try:
            filas, cols = int(input("Filas: ")), int(input("Columnas: "))
            if filas > 0 and cols > 0:
                break
            print("Usa números mayores a 0.")
        except ValueError:
            print("Solo números enteros.")

    sala = crear_sala(filas, cols)

    while True:
        op = input("\n1.Mostrar 2.Reservar 3.Liberar 4.Contar 5.Salir\nOpción: ").strip()
        if op == "1":
            mostrar_sala(sala)
        elif op == "2":
            cambiar_estado(sala, "L", "X", "Reservado.", "Ya está ocupado.")
        elif op == "3":
            cambiar_estado(sala, "X", "L", "Liberado.", "Ya está libre.")
        elif op == "4":
            estadisticas(sala)
        elif op == "5":
            break
        else:
            print("Opción inválida.")


if __name__ == "__main__":
    menu()
