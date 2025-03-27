### **Instrucciones para usarlo**

1️⃣ **Crea una hoja llamada "Plantilla"** con el formato que deseas.  
2️⃣ **Abre VBA** (`ALT + F11`).  
3️⃣ **En el menú**, selecciona **Insertar → Módulo**.  
4️⃣ **Copia y pega el código**.  
5️⃣ **Ejecuta el código (`F5`)**.

 **Resultado:** Se crean **88 hojas**, cada una con el formato de la "Plantilla", y renombradas con los años de 1858 a 1945. 



```c
Sub CrearHojasConFormato()
    Dim i As Integer
    
    ' Verificar si existe la hoja Plantilla "Año 1880"
    If Not SheetExists("Año 1880") Then
        MsgBox "No existe una hoja llamada 'Plantilla'. Crea una antes de ejecutar el código.", vbExclamation, "Error"
        Exit Sub
    End If
    
    ' Eliminar hojas existentes excepto la Plantilla "Año 1880"
    Application.DisplayAlerts = False
    Dim ws As Worksheet
    For Each ws In ThisWorkbook.Sheets
        If ws.Name <> "Año 1880" Then ws.Delete
    Next ws
    Application.DisplayAlerts = True

    ' Crear copias de la hoja Plantilla "Año 1880"
     y renombrarlas con los años
    For i = 1880 To 1899
        Sheets("Año 1880").Copy After:=Sheets(Sheets.Count)
        ActiveSheet.Name = i
    Next i

    MsgBox "Se han creado 22 hojas con formato correctamente.", vbInformation, "Proceso Completado"
End Sub

' Función auxiliar para verificar si una hoja existe
Function SheetExists(sheetName As String) As Boolean
    Dim ws As Worksheet
    On Error Resume Next
    Set ws = ThisWorkbook.Sheets(sheetName)
    SheetExists = Not ws Is Nothing
    On Error GoTo 0
End Function


```


### Corrección codigo se actualiza para que la plantilla tenga la palabra Año

```c
Sub CrearHojasConFormato()
    Dim i As Integer
    Dim ws As Worksheet

    ' Verificar si existe la hoja Plantilla "Año 1902"
    If Not SheetExists("Año 1902") Then
        MsgBox "No existe una hoja llamada 'Año 1902'. Crea una antes de ejecutar el código.", vbExclamation, "Error"
        Exit Sub
    End If

    ' Eliminar hojas existentes excepto la Plantilla "Año 1902"
    Application.DisplayAlerts = False
    For Each ws In ThisWorkbook.Worksheets
        If ws.Name <> "Año 1902" Then ws.Delete ' Evita borrar la plantilla
    Next ws
    Application.DisplayAlerts = True

    ' Crear copias de la hoja Plantilla "Año 1902" y renombrarlas con los años
    For i = 1903 To 1923
        Sheets("Año 1902").Copy After:=Sheets(Sheets.Count)
        ActiveSheet.Name = "Año " & i
    Next i

    MsgBox "Se han creado 21 hojas con formato correctamente.", vbInformation, "Proceso Completado"
End Sub

' Función auxiliar para verificar si una hoja existe
Function SheetExists(sheetName As String) As Boolean
    Dim ws As Worksheet
    On Error Resume Next
    Set ws = ThisWorkbook.Sheets(sheetName)
    SheetExists = Not ws Is Nothing
    On Error GoTo 0
End Function

```


### Modificación código en la fila 1 columna A itera el valor de año por el consecutivo según la plantilla

```C
Sub CrearHojasConFormato()
    Dim i As Integer
    Dim ws As Worksheet
    Dim nuevaHoja As Worksheet

    ' Verificar si existe la hoja Plantilla "Año 1924"
    If Not SheetExists("Año 1924") Then
        MsgBox "No existe una hoja llamada 'Año 1924'. Crea una antes de ejecutar el código.", vbExclamation, "Error"
        Exit Sub
    End If

    ' Eliminar hojas existentes excepto la Plantilla "Año 1924"
    Application.DisplayAlerts = False
    For Each ws In ThisWorkbook.Worksheets
        If ws.Name <> "Año 1924" Then ws.Delete ' Evita borrar la plantilla
    Next ws
    Application.DisplayAlerts = True

    ' Crear copias de la hoja Plantilla "Año 1924", renombrarlas y establecer título en A1
    For i = 1925 To 1945 ' Comienza en 1925 para evitar duplicar la plantilla
        Sheets("Año 1924").Copy After:=Sheets(Sheets.Count)
        Set nuevaHoja = ActiveSheet
        nuevaHoja.Name = "Año " & i
        nuevaHoja.Range("A1").Value = "ANALES_" & i ' Escribir el título en A1
    Next i

    MsgBox "Se han creado 22 hojas con formato correctamente.", vbInformation, "Proceso Completado"
End Sub

' Función auxiliar para verificar si una hoja existe
Function SheetExists(sheetName As String) As Boolean
    Dim ws As Worksheet
    On Error Resume Next
    Set ws = ThisWorkbook.Sheets(sheetName)
    SheetExists = Not ws Is Nothing
    On Error GoTo 0
End Function


```