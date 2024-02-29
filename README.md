# Mi-aplicaci-n-Materiales-App
Aplicación destinada a la rama de Ingeniería en Materiales.


from kivy.app import App
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.label import Label
from kivy.uix.button import Button
from kivy.uix.popup import Popup
from kivy.uix.screenmanager import ScreenManager, Screen
from kivy.uix.scrollview import ScrollView
from kivy.uix.textinput import TextInput

class WelcomeScreen(BoxLayout):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.orientation = 'vertical'
        self.add_widget(Label(text='Bienvenido', size_hint_y=None, height=100))

        opciones_layout = BoxLayout(orientation='vertical')
        base_datos_button = Button(text='Base de Datos de Materiales', size_hint_y=None, height=50)
        base_datos_button.bind(on_press=self.mostrar_base_datos)
        opciones_layout.add_widget(base_datos_button)

        calculadora_button = Button(text='Calculadora de Materiales', size_hint_y=None, height=50)
        calculadora_button.bind(on_press=self.mostrar_calculadora)
        opciones_layout.add_widget(calculadora_button)

        self.add_widget(opciones_layout)

    def mostrar_base_datos(self, instance):
        base_datos_info = """
1. Acero
   - Tipo: Metal
   - Dureza: 8.5 
   - Resistencia: 9.2 
   - Conductividad térmica: 50.2 W/m°C
   - Conductividad eléctrica: 8.4 x 10^6 S/m
   - Temperatura máxima: 800°C
   - Densidad: 7850 kg/m³

2. Aluminio
   - Tipo: Metal
   - Dureza: 5.6
   - Resistencia: 6.8
   - Conductividad térmica: 210.0 W/m°C
   - Conductividad eléctrica: 3.5 x 10^7 S/m
   - Temperatura máxima: 600°C
   - Densidad: 2700 kg/m³

3. Plástico
   - Tipo: Polímero
   - Dureza: 2.3
   - Resistencia: 3.1
   - Conductividad térmica: 0.2 W/m°C
   - Conductividad eléctrica: 10^-16 S/m
   - Temperatura máxima: 150°C
   - Densidad: 900 kg/m³

4. Madera
   - Tipo: Material natural
   - Dureza: 4.7
   - Resistencia: 5.3
   - Conductividad térmica: 0.12 W/m°C
   - Conductividad eléctrica: 10^-16 S/m
   - Temperatura máxima: 250°C
   - Densidad: 700 kg/m³

5. Cobre
   - Tipo: Metal
   - Dureza: 6.9
   - Resistencia: 9.5
   - Conductividad térmica: 401.0 W/m°C
   - Conductividad eléctrica: 5.8 x 10^7 S/m
   - Temperatura máxima: 1000°C
   - Densidad: 8940 kg/m³

6. Vidrio
   - Tipo: Cerámico
   - Dureza: 8.3
   - Resistencia: 6.7
   - Conductividad térmica: 0.8 W/m°C
   - Conductividad eléctrica: 10^-16 S/m
   - Temperatura máxima: 500°C
   - Densidad: 2500 kg/m³

7. Hierro
   - Tipo: Metal
   - Dureza: 4.0
   - Resistencia: 7.8
   - Conductividad térmica: 79.5 W/m°C
   - Conductividad eléctrica: 1.0 x 10^7 S/m
   - Temperatura máxima: 1538°C
   - Densidad: 7874 kg/m³

8. Polietileno
   - Tipo: Polímero
   - Dureza: 2.0
   - Resistencia: 3.0
   - Conductividad térmica: 0.4 W/m°C
   - Conductividad eléctrica: 10^-16 S/m
   - Temperatura máxima: 80°C
   - Densidad: 940 kg/m³

9. Oro
   - Tipo: Metal
   - Dureza: 2.5
   - Resistencia: 7.0
   - Conductividad térmica: 318.0 W/m°C
   - Conductividad eléctrica: 4.1 x 10^7 S/m
   - Temperatura máxima: 1064°C
   - Densidad: 19320 kg/m³

10. Titanio
    - Tipo: Metal
    - Dureza: 6.0
    - Resistencia: 7.0
    - Conductividad térmica: 21.9 W/m°C
    - Conductividad eléctrica: 1.0 x 10^6 S/m
    - Temperatura máxima: 1668°C
    - Densidad: 4500 kg/m³
"""



      # Crear ScrollView y ajustar el tamaño del contenido
        scrollview = ScrollView(size_hint=(None, None), size=(600, 400))
        base_datos_content = Label(text=base_datos_info, size_hint_y=None, markup=True)
        base_datos_content.bind(texture_size=base_datos_content.setter('size'))
        scrollview.add_widget(base_datos_content)

        popup = Popup(title='Base de Datos de Materiales',
                      content=scrollview,
                      size_hint=(None, None), size=(600, 400))
        popup.open()

    def mostrar_calculadora(self, instance):
        popup_content = BoxLayout(orientation='vertical')

        modulo_young_button = Button(text='Calcular Módulo de Young', size_hint_y=None, height=50)
        modulo_young_button.bind(on_press=self.mostrar_modulo_young_input)
        popup_content.add_widget(modulo_young_button)

        resistencia_button = Button(text='Calcular Resistencia a la Tracción', size_hint_y=None, height=50)
        resistencia_button.bind(on_press=self.mostrar_resistencia_traccion_input)
        popup_content.add_widget(resistencia_button)

        conductividad_button = Button(text='Calcular Conductividad Térmica', size_hint_y=None, height=50)
        conductividad_button.bind(on_press=self.mostrar_conductividad_termica_input)
        popup_content.add_widget(conductividad_button)

        densidad_button = Button(text='Calcular Densidad', size_hint_y=None, height=50)
        densidad_button.bind(on_press=self.mostrar_densidad_input)
        popup_content.add_widget(densidad_button)

        popup = Popup(title='Calculadora de Materiales',
                      content=popup_content,
                      size_hint=(None, None), size=(400, 300))
        popup.open()

    def mostrar_modulo_young_input(self, instance):
        self.mostrar_input_popup('Módulo de Young', 'Tensión (σ) [Pa]:', 'Deformación (ε) [m/m]:')

    def mostrar_resistencia_traccion_input(self, instance):
        self.mostrar_input_popup('Resistencia a la Tracción', 'Fuerza (F) [N]:', 'Área (A) [m²]:')

    def mostrar_conductividad_termica_input(self, instance):
        self.mostrar_input_popup('Conductividad Térmica', 'Carga calorífica (Q) [J]:', 'Longitud (L) [m]:', 'Área (A) [m²]:', 'Variación de temperatura (ΔT) [°C]:')

    def mostrar_densidad_input(self, instance):
        self.mostrar_input_popup('Densidad', 'Masa (m) [kg]:', 'Volumen (V) [m³]:')

    def mostrar_input_popup(self, title, *labels):
        popup_content = BoxLayout(orientation='vertical')

        input_container = BoxLayout(orientation='vertical')
        popup_content.add_widget(input_container)

        inputs = []
        for label_text in labels:
            input_layout = BoxLayout(orientation='horizontal')
            input_container.add_widget(input_layout)

            input_layout.add_widget(Label(text=label_text))

            inputs.append(TextInput(hint_text='Ingrese un valor', multiline=False, size_hint_x=0.5))
            input_layout.add_widget(inputs[-1])

        calcular_button = Button(text='Calcular', size_hint_y=None, height=50)
        calcular_button.bind(on_press=lambda instance: self.calcular_resultado(title, *[input.text for input in inputs]))
        popup_content.add_widget(calcular_button)

        popup = Popup(title=title,
                      content=popup_content,
                      size_hint=(None, None), size=(500, 300))
        popup.open()

    def calcular_resultado(self, title, *values):
        if title == 'Módulo de Young':
            resultado = f'Módulo de Young calculado: {float(values[0]) / float(values[1])} Pa'
        elif title == 'Resistencia a la Tracción':
            resultado = f'Resistencia a la Tracción calculada: {float(values[0]) / float(values[1])} N/m²'
        elif title == 'Conductividad Térmica':
            resultado = f'Conductividad Térmica calculada: {(float(values[0]) * float(values[1])) / (float(values[2]) * float(values[3]))} W/m°C'
        elif title == 'Densidad':
            resultado = f'Densidad calculada: {float(values[0]) / float(values[1])} kg/m³'
        else:
            resultado = 'Operación no soportada'

        resultado_popup = Popup(title='Resultado',
                                content=Label(text=resultado),
                                size_hint=(None, None), size=(400, 200))
        resultado_popup.open()

class MyApp(App):
    def build(self):
        sm = ScreenManager()

        welcome_screen = Screen(name='welcome')
        welcome_screen.add_widget(WelcomeScreen())
        sm.add_widget(welcome_screen)

        return sm

if __name__ == '__main__':
    MyApp().run()
