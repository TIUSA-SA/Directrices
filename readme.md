## Nomenglaturas

### Tablas bases de datos

~~~
tbl__NOMBRE_TABLA
~~~

### Formularios
~~~
frm__NOMBRE-MODULO_nombreFormulario
~~~

### Elementos

~~~
lblNombre       //Labels
comboNombre     //ComboBox
txtNombre       //TextBox
btnNombre       //Button
~~~

## Botones

### Colores

|                Boton                          |      Casos            |    Color     | Color letra  |
|-----------------------------------------------|-----------------------|--------------|--------------|
|![Boton salir](/Images/BotonSalir.png)         |/Eliminar/salir        |@Danger       |@activeBorder |
|![Boton consultar](/Images/BotonConsultar.png) |Nuevo/agregar/Guardar  |@primary      |@activeBorder |
|![Boton Excel](/Images/BotonExcel.png)         |Exportacion a Excel    |@success      |@activeBorder |
|![Boton Editar](/Images/BotonOtro.png)         |Editar/Otros           |DarkOrange    |@activeBorder |
|![Boton Editar](/Images/BotonMorado.png)       |Buscar                 |SlateBlue     |@activeBorder |
|![Boton Cancelar](/Images/Cancelar.jpeg)       |Cancelar               |0, 0, 0       |@activeBorder |
|![Boton Editar](/Images/Nuevo.jpeg)            |Nuevo                  |Chartreuse    |0, 0, 0       |
|![Boton Editar](/Images/Guardar.jpeg)          |Guardar                |255, 167, 0   |0, 0, 0       |
  

### Tamaño

Medidas **100, 37** (pixeles)

## Proyectos

### Tipo
![Tipo de proyecto](/Images/TipoProyecto.png)

### Formularios/ventanas
![Ventanas](/Images/Window.png)


### Estructura Home
![Estructura Home](/Images/pantallaHome1.png)
~~~
NavigationBar.Dock = left;
menuBar.Dock = top;
~~~

### Formatos especiales paneles
Formato especial para la organizacion de formularios con paneles
![paneles](/Images/Paneles.png)


## DataGridView

### Formatos

- Claves primarias: Textos centrados
    ~~~
    e.CellStyle.Alignment = DataGridViewContentAlignment.MiddleCenter;
    ~~~
- Numeros: Pegados a la derecha con dos numeros despues del punto decimal y con comas para separa cientos, miles y millones 
    ~~~
    e.CellStyle.Alignment = DataGridViewContentAlignment.MiddleRight;
    e.Value = valor.ToString("N2");
    e.Value = valor2.ToString("N0", CultureInfo.CurrentCulture);
    e.FormattingApplied = true;
    ~~~
- Cantidades de dinero: Pegados a la izquierda, dos numeros despues del punto decimal y signo de pesos
    ~~~
    if (Decimal.TryParse(e.Value.ToString(), out valor))
    {
        CultureInfo cultura = new CultureInfo("es-MX");

        e.Value = valor.ToString("C2", cultura);
        e.FormattingApplied = true;
        e.CellStyle.Alignment = DataGridViewContentAlignment.MiddleRight;
    }
    ~~~
Ejemplo de codigo completo

~~~
private void dataGridView1_CellFormatting(object sender, DataGridViewCellFormattingEventArgs e)
{
    try
    {
        if (rbtnMontos.Checked || rbtnOperador.Checked)
        {
            if (e.ColumnIndex == 8 || e.ColumnIndex == 7)
            {
                e.CellStyle.Alignment = DataGridViewContentAlignment.MiddleCenter;
            }
        }
        else
        {
            if (e.ColumnIndex == 6 || e.ColumnIndex == 7 || e.ColumnIndex == 8 || e.ColumnIndex == 9 || e.ColumnIndex == 15 || e.ColumnIndex == 16 || e.ColumnIndex == 21 || e.ColumnIndex == 22)
            {
                e.CellStyle.Alignment = DataGridViewContentAlignment.MiddleCenter;
            }
        }

        if (dataGridView1.Rows.Count == 0) return;

        if (e.Value == null) return;

        decimal valor;

        if (!Decimal.TryParse(e.Value.ToString(), out valor))
        {
            return;
        }


        if (rbtnMontos.Checked || rbtnOperador.Checked)
        {
            var column = dataGridView1.Columns["Sueldo total del periodo"];
            if (e.ColumnIndex == 3 || e.ColumnIndex == 4 || e.ColumnIndex == 5 || e.ColumnIndex == 6)
            {
                if (Decimal.TryParse(e.Value.ToString(), out valor))
                {
                    CultureInfo cultura = new CultureInfo("es-MX");

                    e.Value = valor.ToString("C2", cultura);
                    e.FormattingApplied = true;

                    e.CellStyle.Alignment = DataGridViewContentAlignment.MiddleRight;
                }
            }

            if (e.ColumnIndex == 0)
                e.CellStyle.Alignment = DataGridViewContentAlignment.MiddleRight;
        }
        else
        {
            var operatorColumn = dataGridView1.Columns["Sueldo del operador"];

            // Asegúrate de que no hay conflictos con la columna del "Sueldo del operador"
            if (operatorColumn != null && e.ColumnIndex == operatorColumn.Index)
            {
                if (Decimal.TryParse(e.Value.ToString(), out valor))
                {
                    CultureInfo cultura = new CultureInfo("es-MX");

                    e.Value = valor.ToString("C2", cultura);
                    e.FormattingApplied = true;
                    e.CellStyle.Alignment = DataGridViewContentAlignment.MiddleRight;
                }
            }
            // Revisa las columnas centradas

            // Revisa las columnas alineadas a la derecha
            else if (e.ColumnIndex == 0 || e.ColumnIndex == 1 || e.ColumnIndex == 4 || e.ColumnIndex == 5 || e.ColumnIndex == 10 || e.ColumnIndex == 11 || e.ColumnIndex == 12 || e.ColumnIndex == 13 || e.ColumnIndex == 14 || e.ColumnIndex == 18 || e.ColumnIndex == 19 || e.ColumnIndex == 20)
            {
                e.CellStyle.Alignment = DataGridViewContentAlignment.MiddleRight;

                // Aplica formato adicional a columnas específicas
                if (e.ColumnIndex == 18 || e.ColumnIndex == 19 || e.ColumnIndex == 20)
                {
                    if (e.Value != null && Decimal.TryParse(e.Value.ToString(), out valor))
                    {
                        e.Value = valor.ToString("N2");
                        e.FormattingApplied = true;
                    }
                }
                else if (e.ColumnIndex == 10 || e.ColumnIndex == 11 || e.ColumnIndex == 12 || e.ColumnIndex == 13 || e.ColumnIndex == 14)
                {
                    if (decimal.TryParse(e.Value.ToString(), out decimal valor2))
                    {
                        // Aplica el formato "N0" para mostrar números enteros con separadores de miles y sin decimales
                        e.Value = valor2.ToString("N0", CultureInfo.CurrentCulture);
                        e.FormattingApplied = true;
                    }
                }
            }
        }
    }
    catch (Exception ex)
    {
        MessageBox.Show("Error: " + ex.Message);
        throw;
    }
}

~~~

### Anchos minimos y maximos de columnas
No se tiene definido un ancho minimo y maximo de las columnas ya que dependera del contenido de cada tabla pero se puede aplicar de la siguiente manera: 
~~~
private void EstablecerAnchoMaximoColumnas(DataGridView dataGridView)
{
    try
    {
        foreach (DataGridViewColumn column in dataGridView.Columns)
        {
            column.MaximumWidth = 300;
            column.MinimumWidth = 100;
        }
    }
    catch (Exception ex)
    {
        MessageBox.Show("Error: " + ex.Message);
        throw;
    }
}
~~~