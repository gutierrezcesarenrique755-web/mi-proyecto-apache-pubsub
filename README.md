"""
Proyecto Apache + PubSub - eventos-app
Licencia: Apache 2.0
Autor: Enrrique
"""

class PubSub:
    def __init__(self):
        self.suscriptores = {}

    def suscribir(self, canal, funcion):
        if canal not in self.suscriptores:
            self.suscriptores[canal] = []
        self.suscriptores[canal].append(funcion)
        print(f"[Suscrito a {canal}]")

    def publicar(self, canal, mensaje):
        print(f"\n[Publicando en {canal}]: {mensaje}")
        if canal in self.suscriptores:
            for funcion in self.suscriptores[canal]:
                funcion(mensaje)

def procesar_evento(mensaje):
    print(f" -> ¡Mensaje recibido! Procesando: {mensaje}")

# --- Inicio del programa ---
print("=== INICIANDO PROYECTO APACHE + PUBSUB ===")

bus = PubSub()
bus.suscribir("eventos-app", procesar_evento)

bus.publicar("eventos-app", {'tipo': 'usuario.registrado', 'usuario': 'Enrrique'})
bus.publicar("eventos-app", {'tipo': 'pago.completado', 'monto': 250})

print("\n=== PROYECTO FUNCIONANDO CON LICENCIA APACHE 2.0 ===")
