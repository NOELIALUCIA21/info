# info
# ============================================
# SISTEMA DE GESTIÓN DE INVENTARIOS
# Autor: Noelia
# Descripción: Sistema simple para gestionar
# productos de una tienda utilizando POO.
# ============================================


# =========================
# CLASE PRODUCTO
# =========================
class Producto:
    """
    Clase que representa un producto en el inventario.
    Cada producto tiene:
    - ID único
    - Nombre
    - Cantidad
    - Precio
    """

    def __init__(self, id_producto, nombre, cantidad, precio):
        self.__id = id_producto        # Atributo privado
        self.__nombre = nombre
        self.__cantidad = cantidad
        self.__precio = precio

    # ===== GETTERS =====
    def get_id(self):
        return self.__id

    def get_nombre(self):
        return self.__nombre

    def get_cantidad(self):
        return self.__cantidad

    def get_precio(self):
        return self.__precio

    # ===== SETTERS =====
    def set_nombre(self, nombre):
        self.__nombre = nombre

    def set_cantidad(self, cantidad):
        self.__cantidad = cantidad

    def set_precio(self, precio):
        self.__precio = precio

    def __str__(self):
        """
        Método especial para mostrar el producto
        de forma organizada.
        """
        return f"ID: {self.__id} | Nombre: {self.__nombre} | Cantidad: {self.__cantidad} | Precio: ${self.__precio:.2f}"


# =========================
# CLASE INVENTARIO
# =========================
class Inventario:
    """
    Clase que gestiona la lista de productos.
    """

    def __init__(self):
        self.productos = []  # Lista donde se almacenan los productos

    # Añadir producto asegurando ID único
    def agregar_producto(self, producto):
        for p in self.productos:
            if p.get_id() == producto.get_id():
                print("❌ Error: El ID ya existe.")
                return
        self.productos.append(producto)
        print("✅ Producto agregado correctamente.")

    # Eliminar producto por ID
    def eliminar_producto(self, id_producto):
        for p in self.productos:
            if p.get_id() == id_producto:
                self.productos.remove(p)
                print("✅ Producto eliminado.")
                return
        print("❌ Producto no encontrado.")

    # Actualizar producto
    def actualizar_producto(self, id_producto, nueva_cantidad=None, nuevo_precio=None):
        for p in self.productos:
            if p.get_id() == id_producto:
                if nueva_cantidad is not None:
                    p.set_cantidad(nueva_cantidad)
                if nuevo_precio is not None:
                    p.set_precio(nuevo_precio)
                print("✅ Producto actualizado correctamente.")
                return
        print("❌ Producto no encontrado.")

    # Buscar producto por nombre
    def buscar_por_nombre(self, nombre):
        encontrados = []
        for p in self.productos:
            if nombre.lower() in p.get_nombre().lower():
                encontrados.append(p)

        if encontrados:
            print("🔍 Productos encontrados:")
            for p in encontrados:
                print(p)
        else:
            print("❌ No se encontraron productos con ese nombre.")

    # Mostrar todos los productos
    def mostrar_productos(self):
        if not self.productos:
            print("📦 Inventario vacío.")
        else:
            print("\n📋 LISTA DE PRODUCTOS:")
            for p in self.productos:
                print(p)


# =========================
# MENÚ INTERACTIVO
# =========================
def menu():
    inventario = Inventario()

    while True:
        print("\n====== SISTEMA DE INVENTARIO ======")
        print("1. Agregar producto")
        print("2. Eliminar producto")
        print("3. Actualizar producto")
        print("4. Buscar producto por nombre")
        print("5. Mostrar todos los productos")
        print("6. Salir")

        opcion = input("Seleccione una opción: ")

        if opcion == "1":
            try:
                id_producto = input("Ingrese ID: ")
                nombre = input("Ingrese nombre: ")
                cantidad = int(input("Ingrese cantidad: "))
                precio = float(input("Ingrese precio: "))
                producto = Producto(id_producto, nombre, cantidad, precio)
                inventario.agregar_producto(producto)
            except ValueError:
                print("❌ Error: Ingrese valores numéricos válidos.")

        elif opcion == "2":
            id_producto = input("Ingrese ID del producto a eliminar: ")
            inventario.eliminar_producto(id_producto)

        elif opcion == "3":
            id_producto = input("Ingrese ID del producto a actualizar: ")
            try:
                cantidad = input("Nueva cantidad (dejar vacío si no desea cambiar): ")
                precio = input("Nuevo precio (dejar vacío si no desea cambiar): ")

                nueva_cantidad = int(cantidad) if cantidad else None
                nuevo_precio = float(precio) if precio else None

                inventario.actualizar_producto(id_producto, nueva_cantidad, nuevo_precio)
            except ValueError:
                print("❌ Error: Valores numéricos inválidos.")

        elif opcion == "4":
            nombre = input("Ingrese nombre a buscar: ")
            inventario.buscar_por_nombre(nombre)

        elif opcion == "5":
            inventario.mostrar_productos()

        elif opcion == "6":
            print("👋 Saliendo del sistema...")
            break

        else:
            print("❌ Opción inválida. Intente nuevamente.")


# Ejecutar programa
if __name__ == "__main__":
    menu()
