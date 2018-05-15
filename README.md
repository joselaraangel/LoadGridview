# LoadDataGrid

Imports System.Data
Imports System.Data.SqlClient

Partial Class _Default
    Inherits Page

    Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs)


    End Sub

    Function GetData(ByVal queryString As String) As DataSet

        Dim connectionString As String = "Data Source=JOSE;Initial Catalog=Ordenes;Integrated Security=True;"

        Dim ds As New DataSet()

        Try

            Dim connection As New SqlConnection(connectionString)
            Dim adapter As New SqlDataAdapter(queryString, connection)

            adapter.Fill(ds)


        Catch ex As Exception

            'Message.Text = "Unable to connect to the database."

        End Try

        Return ds

    End Function

    Protected Sub GridView1_SelectedIndexChanged(sender As Object, e As EventArgs) Handles GridView1.SelectedIndexChanged

    End Sub
    Protected Sub btnBuscar_Click(sender As Object, e As EventArgs) Handles btnBuscar.Click

        Dim queryString As String =
            "Select * From [Ordenes].[dbo].[Productos]"

        If (TxtProducto.Text <> "") Then
            queryString += " where PKProducto = '" + TxtProducto.Text + "'"
        End If

        If (TxtNombre.Text <> "") Then
            queryString += " where Nomb_Prod = '" + TxtNombre.Text + "'"
        End If


        Dim i As String = queryString

        Dim ds As DataSet = GetData(queryString)
        If (ds.Tables.Count > 0) Then

            GridView1.DataSource = ds
            GridView1.DataBind()

        Else

            'Message.Text = "Unable to connect to the database."

        End If

    End Sub
End Class