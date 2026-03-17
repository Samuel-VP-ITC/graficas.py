# graficas.py
Se creó una ventana gráfica que genera 4 tipos de graficas diferentes

## 🚀 Características
Gráfica de Barras: Comparativa de ventas por producto.

Gráfica de Líneas: Seguimiento de tendencias de rendimiento mensual.

Gráfica de Dispersión: Visualización de muestreo aleatorio de sensores.

Gráfica de Pastel: Distribución porcentual de recursos.

## 🛠️ Tecnologías Utilizadas
Python: Lenguaje base.

Flet: Framework para la interfaz de usuario (basado en Flutter).

Matplotlib: Generación de gráficos estadísticos.

Flet-Charts: Integración de figuras de Matplotlib en componentes de Flet.

## 🧠 Explicación del Código

Backend de Gráficos: Cada función (ej. generar_grafica_barras) crea un objeto figure de Matplotlib.

Integración: Usamos fch.MatplotlibChart(figure=fig) para convertir el gráfico en un widget que Flet pueda renderizar.

Layout: Se utiliza un GridView con runs_count=2 para organizar los gráficos en una cuadrícula simétrica de dos columnas.

'''
import matplotlib.pyplot as plt
import flet as ft
import flet_charts as fch
import random

# --- FUNCIONES DE GRÁFICAS ---

def generar_grafica_barras():
    productos = ["A", "B", "C", "D"]
    ventas = [15, 30, 45, 10]
    fig, ax = plt.subplots(figsize=(4, 3))
    ax.bar(productos, ventas, color="skyblue")
    ax.set_title("Ventas por Producto", fontsize=10, weight='bold')
    plt.tight_layout()
    return fig

def generar_grafica_lineas():
    meses = ["Ene", "Feb", "Mar", "Abr", "May"]
    rendimiento = [10, 25, 18, 40, 35]
    fig, ax = plt.subplots(figsize=(4, 3))
    ax.plot(meses, rendimiento, color="orange", marker="o", linewidth=2)
    ax.set_title("Tendencia de Rendimiento", fontsize=10, weight='bold')
    ax.grid(True, linestyle='--', alpha=0.6)
    plt.tight_layout()
    return fig

def generar_grafica_dispersion():
    x = [i for i in range(20)]
    y = [random.randint(10, 50) for _ in range(20)]
    fig, ax = plt.subplots(figsize=(4, 3))
    ax.scatter(x, y, color="purple", alpha=0.6, edgecolors="white")
    ax.set_title("Muestreo de Sensores", fontsize=10, weight='bold')
    plt.tight_layout()
    return fig

# --- NUEVA FUNCIÓN: GRÁFICA DE PASTEL ---
def generar_grafica_pastel():
    etiquetas = ['Recursos A', 'Recursos B', 'Recursos C']
    tamanos = [40, 35, 25]
    colores = ['#ff9999','#66b3ff','#99ff99']
    
    fig, ax = plt.subplots(figsize=(4, 3))
    ax.pie(tamanos, labels=etiquetas, autopct='%1.1f%%', startangle=90, colors=colores)
    ax.set_title("Distribución de Recursos", fontsize=10, weight='bold')
    plt.tight_layout()
    return fig

def main(page: ft.Page):
    page.title = "Dashboard TAP - Final"
    page.theme_mode = "light"
    page.vertical_alignment = "start"
    page.horizontal_alignment = "center"

    header = ft.Text("Dashboard de Visualización Completo", size=24, weight="bold")

    tablero = ft.GridView(
        expand=True,
        runs_count=2,
        spacing=20,
        run_spacing=20,
        child_aspect_ratio=1.5,
    )

    # Gráfica 1: Barras
    fig_1 = generar_grafica_barras()
    contenedor_1 = ft.Container(content=fch.MatplotlibChart(figure=fig_1), border=ft.border.all(1, "black12"), border_radius=10, padding=5)
    plt.close(fig_1)

    # Gráfica 2: Líneas
    fig_2 = generar_grafica_lineas()
    contenedor_2 = ft.Container(content=fch.MatplotlibChart(figure=fig_2), border=ft.border.all(1, "black12"), border_radius=10, padding=5)
    plt.close(fig_2)

    # Gráfica 3: Dispersión
    fig_3 = generar_grafica_dispersion()
    contenedor_3 = ft.Container(content=fch.MatplotlibChart(figure=fig_3), border=ft.border.all(1, "black12"), border_radius=10, padding=5)
    plt.close(fig_3)

    # --- ESPACIO 4: AHORA CON GRÁFICA DE PASTEL ---
    fig_4 = generar_grafica_pastel()
    contenedor_4 = ft.Container(
        content=fch.MatplotlibChart(figure=fig_4), 
        border=ft.border.all(1, "black12"), 
        border_radius=10, 
        padding=5
    )
    plt.close(fig_4)

    # Cargamos todos los controles al tablero
    tablero.controls.append(contenedor_1)
    tablero.controls.append(contenedor_2)
    tablero.controls.append(contenedor_3)
    tablero.controls.append(contenedor_4)

    page.add(header, ft.Divider(), tablero)

if __name__ == "__main__":
    ft.app(target=main)
'''

<img width="1919" height="776" alt="image" src="https://github.com/user-attachments/assets/6976c48a-5df2-4422-bfe0-92cac35c8ca1" />

<img width="1904" height="642" alt="image" src="https://github.com/user-attachments/assets/03dbe111-21cb-4129-96ea-f953250e64c5" />

