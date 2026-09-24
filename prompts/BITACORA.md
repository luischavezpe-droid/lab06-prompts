# Bitacora de prompts

Laboratorio 06: Fundamentos de Ingenieria de Prompts. 
Herramienta de IA usada: (escribe aqui cual usaste) 

## Ejercicio 2: Tokens y ventana de contexto

| Texto | Caracteres | Tokens |
| --- | --- | --- |
| Los estudiantes programan en Java. | 34| 7|
| The students program in Java. | 29| 6|
| desafortunadamente | 18| 4|

Preguntas 4 y 5
Se pudo observar como la ia no recuerda nada de lo que se le habia explicado en la anterior recomendacion, esto es por que nunca vio o reconocio ese dato en ese chat, a menos que tenga la opcion de memoria no podria recordarlo

## Ejercicio 3: Temperatura

| Temperatura | % de BiblioTec | Nombres en los 5 intentos |
| ----------- | -------------- | ------------------------- |
| 0           | 100.0%         | BiblioTec, BiblioTec, BiblioTec, BiblioTec, BiblioTec |
| 0.5         | 65.3%          | BiblioTec, BiblioTec, LibroYa, BiblioTec, LibroYa |
| 1           | 44.5%          | BiblioTec, PaginaLibre, PrestaLibro, BiblioTec, BiblioTec |
| 1.8         | 32.2%          | BiblioTec, BiblioTec, LibroYa, LibroYa, BiblioTec |

## Ejercicio 4: Prompt vago vs estructurado 

| Criterio | Prompt vago | Prompt estructurado |
| -------- | ----------- | ------------------- |
| Menciona el objetivo del sistema |No |Si |
| Menciona a los usuarios principales |Si |Si    |
| Tiene exactamente 3 funcionalidades |No |Si |
| Esta en 3 parrafos |No |Si |
| Lo usaria en un informe real |No |Si |

## Ejercicio 5: Anatomia de un prompt
| Componente | Texto de mi prompt |
| :--- | :--- |
| **Rol** | Desarrollador de Java.|
| **Instrucción** |Actua como desarrollador Java. Usando una clase Producto con los atributos, codigo, nombre, precio y stock |
| **Contexto** | Crea un programa en Java para gestionar los productos de una tienda |
| **Ejemplo** | Explica primero la estructura de la clase |
| **Formato** | codigo Java. |

### Respuestas del nivel 1 al 5:

en el nivel 1 la IA fue muy directa y no hizo nada que no se pudiese esperar, en el nivel 2 ya demostro un poco 
## Ejercicio 6: Del prompt basico al profesional

| Qué revisar | Cumple (Sí / No) |
| :--- | :--- |
| ¿Está escrito en Java y usa Swing? | si|
| ¿Pide correo y contraseña? |Si |
| ¿Explica el funcionamiento antes o después del código? |antes y despues explica |
| ¿El código está organizado en clases? |Si |
| ¿Valida los datos que ingresa el usuario? | Si|

```text
AuthService.java

package com.ejemplo.login;

import java.util.Arrays;

public class AuthService {

    // Valida que el correo no esté vacío y contenga '@'
    public boolean esEmailValido(String email) {
        return email != null && email.contains("@");
    }

    // Valida que la contraseña tenga al menos 8 caracteres
    public boolean esPasswordValida(char[] password) {
        return password != null && password.length >= 8;
    }

    // Comprueba las credenciales
    public boolean autenticar(String email, char[] password) {
        String passStr = new String(password);
        
        // Credenciales de prueba (la contraseña debe tener al menos 8 caracteres)
        boolean credencialesValidas = "usuario@dominio.com".equals(email) && "12345678".equals(passStr);

        // Limpiar el arreglo de caracteres por seguridad
        Arrays.fill(password, '0');

        return credencialesValidas;
    }
}

LoginFrame.java

package com.ejemplo.login;

import javax.swing.*;
import java.awt.*;

public class LoginFrame extends JFrame {

    private JTextField txtEmail;
    private JPasswordField txtPassword;
    private JButton btnLogin;
    private AuthService authService;

    public LoginFrame() {
        this.authService = new AuthService();
        configurarVentana();
        inicializarComponentes();
    }

    private void configurarVentana() {
        setTitle("Acceso al Sistema");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(380, 220);
        setLocationRelativeTo(null); // Centra la ventana en pantalla
        setResizable(false);
    }

    private void inicializarComponentes() {
        JPanel panel = new JPanel(new GridBagLayout());
        panel.setBorder(BorderFactory.createEmptyBorder(15, 15, 15, 15));
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(5, 5, 5, 5);
        gbc.fill = GridBagConstraints.HORIZONTAL;

        // Campo para Correo
        gbc.gridx = 0; gbc.gridy = 0;
        panel.add(new JLabel("Correo electrónico:"), gbc);

        gbc.gridx = 1; gbc.gridy = 0; gbc.weightx = 1.0;
        txtEmail = new JTextField(15);
        panel.add(txtEmail, gbc);

        // Campo para Contraseña
        gbc.gridx = 0; gbc.gridy = 1; gbc.weightx = 0.0;
        panel.add(new JLabel("Contraseña:"), gbc);

        gbc.gridx = 1; gbc.gridy = 1; gbc.weightx = 1.0;
        txtPassword = new JPasswordField(15);
        panel.add(txtPassword, gbc);

        // Botón de Iniciar Sesión
        gbc.gridx = 0; gbc.gridy = 2; gbc.gridwidth = 2; gbc.fill = GridBagConstraints.NONE;
        gbc.anchor = GridBagConstraints.CENTER;
        btnLogin = new JButton("Iniciar Sesión");
        panel.add(btnLogin, gbc);

        // Evento al hacer clic en el botón
        btnLogin.addActionListener(e -> ejecutarLogin());

        add(panel);
    }

    private void ejecutarLogin() {
        String email = txtEmail.getText().trim();
        char[] password = txtPassword.getPassword();

        // 1. Validar campos vacíos
        if (email.isEmpty() || password.length == 0) {
            JOptionPane.showMessageDialog(this, 
                "Por favor ingrese tanto el correo como la contraseña.", 
                "Campos Incompletos", 
                JOptionPane.WARNING_MESSAGE);
            return;
        }

        // 2. Validar que el correo contenga '@'
        if (!authService.esEmailValido(email)) {
            JOptionPane.showMessageDialog(this, 
                "El correo electrónico debe contener un símbolo '@'.", 
                "Correo Inválido", 
                JOptionPane.ERROR_MESSAGE);
            return;
        }

        // 3. Validar que la contraseña tenga al menos 8 caracteres
        if (!authService.esPasswordValida(password)) {
            JOptionPane.showMessageDialog(this, 
                "La contraseña debe tener al menos 8 caracteres.", 
                "Contraseña Débilitada", 
                JOptionPane.WARNING_MESSAGE);
            return;
        }

        // 4. Autenticar credenciales
        if (authService.autenticar(email, password)) {
            JOptionPane.showMessageDialog(this, 
                "¡Autenticación exitosa! Bienvenido al sistema.", 
                "Éxito", 
                JOptionPane.INFORMATION_MESSAGE);
            
            this.dispose(); // Cierra la ventana de login
        } else {
            JOptionPane.showMessageDialog(this, 
                "Credenciales incorrectas. Verifique correo y contraseña.", 
                "Error de Autenticación", 
                JOptionPane.ERROR_MESSAGE);
            txtPassword.setText(""); // Limpia la contraseña ingresada
        }
    }
}

Main.java

package com.ejemplo.login;

import javax.swing.SwingUtilities;

public class Main {

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            LoginFrame frame = new LoginFrame();
            frame.setVisible(true);
        });
    }
}
```


