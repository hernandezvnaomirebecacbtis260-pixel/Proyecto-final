# Proyecto-final
import tkinter as tk
from tkinter import ttk
from tkinter import messagebox
from PIL import Image, ImageTk

# ---------------------------------------------------------
#     CONFIGURACIÓN PRINCIPAL
# ---------------------------------------------------------

ventana = tk.Tk()
ventana.title("Flor Arte")
ventana.geometry("1000x700")
ventana.configure(bg="#ffffff")

# ---------------------------------------------------------
#     CARGAR LOGO
# ---------------------------------------------------------
try:
    logo_img = Image.open("C:/Users/Ricardo/Downloads/logof.jpeg")
    logo_img = logo_img.resize((120, 120))
    logo = ImageTk.PhotoImage(logo_img)
except:
    logo = None

# ---------------------------------------------------------
#     FUNCIONES PARA CAMBIAR DE PANTALLA
# ---------------------------------------------------------

def mostrar_pantalla(nombre):
    for frame in pantallas.values():
        frame.pack_forget()
    pantallas[nombre].pack(fill="both", expand=True)

# ---------------------------------------------------------
#     ENCABEZADO (BARRA SUPERIOR)
# ---------------------------------------------------------

header = tk.Frame(ventana, bg="#f4b183", height=120)
header.pack(fill="x")

if logo:
    tk.Label(header, image=logo, bg="#f4b183").place(x=10, y=5)

titulo = tk.Label(header, text="Flor Arte", font=("Segoe Script", 28, "bold"), bg="#f4b183")
titulo.place(x=150, y=35)

# Botones del menú
menu_items = ["Inicio", "Login", "Contacto", "Carrito", "Perfil"]
menu_botones = {}

x_pos = 500
for item in menu_items:
    btn = tk.Button(header, text=item, bg="#e69138", fg="white",
                    font=("Arial", 12, "bold"), width=10,
                    command=lambda i=item: mostrar_pantalla(i))
    btn.place(x=x_pos, y=45)
    menu_botones[item] = btn
    x_pos += 110

# ---------------------------------------------------------
#     CONTENEDOR DE PANTALLAS
# ---------------------------------------------------------

pantallas = {
    "Inicio": tk.Frame(ventana, bg="white"),
    "Login": tk.Frame(ventana, bg="white"),
    "Contacto": tk.Frame(ventana, bg="white"),
    "Carrito": tk.Frame(ventana, bg="white"),
    "Perfil": tk.Frame(ventana, bg="white")
}
# ---------------------------------------------------------
#     PANTALLA DE INICIO CON SCROLL (Arreglado)
# ---------------------------------------------------------

pantallas["Inicio"].configure(bg="white")

# --- Crear contenedor con scroll ---
canvas_inicio = tk.Canvas(pantallas["Inicio"], bg="white", highlightthickness=0)
scroll_y = tk.Scrollbar(pantallas["Inicio"], orient="vertical", command=canvas_inicio.yview)
frame_inicio = tk.Frame(canvas_inicio, bg="white")

canvas_inicio.configure(yscrollcommand=scroll_y.set)

canvas_inicio.pack(side="left", fill="both", expand=True)
scroll_y.pack(side="right", fill="y")

canvas_inicio.create_window((0, 0), window=frame_inicio, anchor="nw")

# Actualizar scroll cuando cambie el tamaño
def ajustar_scroll(event):
    canvas_inicio.configure(scrollregion=canvas_inicio.bbox("all"))

frame_inicio.bind("<Configure>", ajustar_scroll)

# --- CONTENIDO DEL INICIO (todo dentro de frame_inicio) ---

# Logo
if logo:
    tk.Label(frame_inicio, image=logo, bg="white").pack(pady=20)

# Título
tk.Label(
    frame_inicio,
    text="Bienvenido a Flor Arte",
    font=("Segoe Script", 30, "bold"),
    bg="white"
).pack(pady=10)

# Bienvenida
tk.Label(
    frame_inicio,
    text="Donde las flores cobran vida en cada detalle,\n"
         "aportando carácter y sensibilidad en cada arreglo floral.",
    font=("Arial", 18),
    bg="white",
    justify="center"
).pack(pady=20)

# Misión
tk.Label(frame_inicio, text="Misión:", font=("Arial", 22, "bold"), bg="white").pack(anchor="w", padx=80, pady=(10, 0))
tk.Label(
    frame_inicio,
    text="Transmitir emociones a través de flores con calidad y dedicación.",
    font=("Arial", 16),
    bg="white",
    justify="left",
    wraplength=800
).pack(anchor="w", padx=80)

# Visión
tk.Label(frame_inicio, text="Visión:", font=("Arial", 22, "bold"), bg="white").pack(anchor="w", padx=80, pady=(20, 0))
tk.Label(
    frame_inicio,
    text="Ser una empresa reconocida por su innovación en el diseño floral,\n"
         "cumpliendo con las necesidades del cliente.",
    font=("Arial", 16),
    bg="white",
    justify="left",
    wraplength=800
).pack(anchor="w", padx=80)

# Ubicación
tk.Label(frame_inicio, text="Ubicación:", font=("Arial", 22, "bold"), bg="white").pack(anchor="w", padx=80, pady=(20, 0))

ubicaciones = [
    "Acayucan, Blvd. del niño poblano #89",
    "Calle por los Mártires #250",
    "San Andrés Tuxtla, Veracruz"
]

for u in ubicaciones:
    tk.Label(
        frame_inicio,
        text="• " + u,
        font=("Arial", 16),
        bg="white",
        justify="left"
    ).pack(anchor="w", padx=110, pady=3)

# Correo
tk.Label(
    frame_inicio,
    text="Correo: FlorArte21@gmail.com",
    font=("Arial", 16),
    bg="white"
).pack(anchor="w", padx=80, pady=(20, 0))

# Teléfono
tk.Label(
    frame_inicio,
    text="Teléfono: 922 807 0564",
    font=("Arial", 16),
    bg="white"
).pack(anchor="w", padx=80, pady=(0, 40))

# ---------------------------------------------------------
#     PANTALLA LOGIN
# ---------------------------------------------------------

login_campos = ["Nombre Completo", "Correo Electrónico", "Dirección", "Número de Celular", "Contraseña"]

entradas_login = {}

tk.Label(pantallas["Login"], text="Formulario de Inicio de Sesión", font=("Arial", 22, "bold"), bg="white").pack(pady=10)

login_frame = tk.Frame(pantallas["Login"], bg="white")
login_frame.pack()

for campo in login_campos:
    tk.Label(login_frame, text=campo + ":", font=("Arial", 14), bg="white").pack(anchor="w")
    entrada = tk.Entry(login_frame, font=("Arial", 14), width=40)
    entrada.pack(pady=5)
    entradas_login[campo] = entrada

tk.Button(pantallas["Login"], text="Registrarse", bg="#e06666", fg="white",
          font=("Arial", 14, "bold"), width=15).pack(pady=20)

# ---------------------------------------------------------
#     PANTALLA DE CONTACTO
# ---------------------------------------------------------

contacto_campos = ["Nombre Completo", "Correo Electrónico", "Asunto del Mensaje"]

entradas_contacto = {}

tk.Label(pantallas["Contacto"], text="Formulario de Contacto", font=("Arial", 22, "bold"), bg="white").pack(pady=10)

contacto_frame = tk.Frame(pantallas["Contacto"], bg="white")
contacto_frame.pack()

for campo in contacto_campos:
    tk.Label(contacto_frame, text=campo + ":", font=("Arial", 14), bg="white").pack(anchor="w")
    entrada = tk.Entry(contacto_frame, width=50, font=("Arial", 14))
    entrada.pack(pady=5)
    entradas_contacto[campo] = entrada

tk.Label(contacto_frame, text="Mensaje:", font=("Arial", 14), bg="white").pack(anchor="w")
mensaje = tk.Text(contacto_frame, width=50, height=5, font=("Arial", 14))
mensaje.pack(pady=5)

tk.Button(pantallas["Contacto"], text="Enviar Mensaje", bg="#6aa84f", fg="white",
          font=("Arial", 14, "bold"), width=15).pack(pady=20)

# ---------------------------------------------------------
#     PANTALLA CARRITO
# ---------------------------------------------------------

productos = ["Rosa Roja", "Ramo Tulipanes", "Caja Floral Premium", "Orquídea Blanca"]
precios = [120, 250, 650, 580]

tk.Label(pantallas["Carrito"], text="Carrito de Compras", font=("Arial", 22, "bold"), bg="white").pack(pady=10)

carrito_frame = tk.Frame(pantallas["Carrito"], bg="white")
carrito_frame.pack()

for i in range(len(productos)):
    tk.Label(carrito_frame, text=f"{productos[i]} — ${precios[i]}", font=("Arial", 16), bg="white").pack(anchor="w", pady=5)

# ---------------------------------------------------------
#     PANTALLA PERFIL
# ---------------------------------------------------------

perfil_campos = ["Editar Nombre", "Editar Correo", "Editar Dirección", "Editar Número", "Cambiar Contraseña"]

entradas_perfil = {}

tk.Label(pantallas["Perfil"], text="Gestión de Perfil", font=("Arial", 22, "bold"), bg="white").pack(pady=20)

perfil_frame = tk.Frame(pantallas["Perfil"], bg="white")
perfil_frame.pack()

for campo in perfil_campos:
    tk.Label(perfil_frame, text=campo + ":", font=("Arial", 14), bg="white").pack(anchor="w")
    entrada = tk.Entry(perfil_frame, font=("Arial", 14), width=40)
    entrada.pack(pady=5)
    entradas_perfil[campo] = entrada

tk.Button(pantallas["Perfil"], text="Guardar Cambios", bg="#3d85c6", fg="white",
          font=("Arial", 14, "bold"), width=15).pack(pady=20)

# ---------------------------------------------------------
#     PIE DE PÁGINA
# ---------------------------------------------------------

footer = tk.Frame(ventana, bg="#f4b183", height=80)
footer.pack(side="bottom", fill="x")

iconos = ["Facebook", "Instagram", "WhatsApp"]
icon_labels = []

x = 20
for icon in iconos:
    lbl = tk.Label(footer, text=icon, bg="#f4b183", font=("Arial", 12, "bold"))
    lbl.place(x=x, y=25)
    x += 120

tk.Label(footer, text="© 2025 Flor Arte — Todos los derechos reservados",
         bg="#f4b183", font=("Arial", 12, "bold")).place(x=500, y=25)

# Mostrar pantalla inicial
mostrar_pantalla("Inicio")

ventana.mainloop()
