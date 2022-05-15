#include "MyForm.h"

using namespace System;
using namespace System::Windows::Forms;
using namespace System::Data::OleDb;

[STAThread]
int main(array<String^>^ arg){
	Application::EnableVisualStyles();
	Application::SetCompatibleTextRenderingDefault(false);

	CRUD::MyForm form;
	Application::Run(% form);
}

System::Void CRUD::MyForm::descargar_btn_Click(System::Object^  sender, System::EventArgs^  e) {

	String^ connectionString = "provider=Microsoft.Jet.OLEDB.4.0;Data Source=Database.mdb";
	OleDbConnection^ dbConnection = gcnew OleDbConnection(connectionString);

	dbConnection->Open();
	String^ query = "SELECT * FROM [table_name]";
	OleDbCommand^dbComand = gcnew OleDbCommand(query, dbConnection);
	OleDbDataReader^ dbReader = dbComand->ExecuteReader();

	if (dbReader->HasRows == false) {
		MessageBox::Show("");

	}
	else {
		while (dbReader->Read()) {
			dataGridView1->Rows->Add(dbReader["id"], dbReader["nombre"]);
			MessageBox::Show("");
		  }
		}

	dbReader->Close();
	dbConnection->Close();

	return System::Void();

}

System::Void CRUD::MyForm::agg_btn_Click(System::Object^  sender, System::EventArgs^  e) {

	if (dataGridView1->SelectedRows->Count != 1 ) {
		MessageBox::Show("");
		return;
	}

	int index = dataGridView1->SelectedRows[0]->Index;


	if (dataGridView1->Rows[index]->Cells[0]->Value == nullptr ||
		dataGridView1->Rows[index]->Cells[1]->Value == nullptr  ) {
		MessageBox::Show("");
		return;
	}

	String^ id = dataGridView1->Rows[index]->Cells[0]->Value->ToString();
	String^ nombre = dataGridView1->Rows[index]->Cells[0]->Value->ToString();
	
	
	String^ connectionString = "provider=Microsoft.Jet.OLEDB.4.0;Data Source=Database.mdb";
	OleDbConnection^ dbConnection = gcnew OleDbConnection(connectionString);

	dbConnection->Open();
	String^ query = "SELECT * FROM [table_name] VALUES (" + id + " , '" + nombre + ")";
	OleDbCommand^dbComand = gcnew OleDbCommand(query, dbConnection);
	OleDbDataReader^ dbReader = dbComand->ExecuteReader();


	if (dbComand -> ExecuteNonQuery() != 1)
		MessageBox::Show("");
	else
		MessageBox::Show("");

	dbConnection->Close();

	return System::Void();
}
System::Void CRUD::MyForm::mod_btn_Click(System::Object^  sender, System::EventArgs^  e) {
	if (dataGridView1->SelectedRows->Count != 1) {
		MessageBox::Show("");
		return;
	}

	int index = dataGridView1->SelectedRows[0]->Index;


	if (dataGridView1->Rows[index]->Cells[0]->Value == nullptr ||
		dataGridView1->Rows[index]->Cells[1]->Value == nullptr) {
		MessageBox::Show("");
		return;
	}

	String^ id = dataGridView1->Rows[index]->Cells[0]->Value->ToString();
	String^ nombre = dataGridView1->Rows[index]->Cells[0]->Value->ToString();


	String^ connectionString = "provider=Microsoft.Jet.OLEDB.4.0;Data Source=Database.mdb";
	OleDbConnection^ dbConnection = gcnew OleDbConnection(connectionString);

	dbConnection->Open();
	String^ query = "UPDATE [table_name] SET Nombre= '"+nombre+"'WHERE id="+id;
	OleDbCommand^dbComand = gcnew OleDbCommand(query, dbConnection);
	OleDbDataReader^ dbReader = dbComand->ExecuteReader();


	if (dbComand->ExecuteNonQuery() != 1)
		MessageBox::Show("");
	else
		MessageBox::Show("");

	dbConnection->Close();

	return System::Void();

}

System::Void CRUD::MyForm::delete_btn_Click(System::Object^  sender, System::EventArgs^  e) {

	if (dataGridView1->SelectedRows->Count != 1) {
		MessageBox::Show("");
		return;
	}

	int index = dataGridView1->SelectedRows[0]->Index;


	if (dataGridView1->Rows[index]->Cells[0]->Value == nullptr ||
		dataGridView1->Rows[index]->Cells[1]->Value == nullptr) {
		MessageBox::Show("");
		return;
	}

	String^ id = dataGridView1->Rows[index]->Cells[0]->Value->ToString();
	String^ nombre = dataGridView1->Rows[index]->Cells[0]->Value->ToString();


	String^ connectionString = "provider=Microsoft.Jet.OLEDB.4.0;Data Source=Database.mdb";
	OleDbConnection^ dbConnection = gcnew OleDbConnection(connectionString);

	dbConnection->Open();
	String^ query = "SELECT * FROM [table_name] VALUES (" + id + " , '" + nombre + ")";
	OleDbCommand^dbComand = gcnew OleDbCommand(query, dbConnection);
	OleDbDataReader^ dbReader = dbComand->ExecuteReader();


	if (dbComand->ExecuteNonQuery() != 1)
		MessageBox::Show("");
	else
		MessageBox::Show("");

	dbConnection->Close();

	return System::Void();
}
System::Void CRUD::MyForm::mod_btn_Click(System::Object^  sender, System::EventArgs^  e) {
	if (dataGridView1->SelectedRows->Count != 1) {
		MessageBox::Show("");
		return;
	}

	int index = dataGridView1->SelectedRows[0]->Index;


	if (dataGridView1->Rows[index]->Cells[1]->Value == nullptr) {
		MessageBox::Show("");
		return;
	}

	String^ id = dataGridView1->Rows[index]->Cells[0]->Value->ToString();
	


	String^ connectionString = "provider=Microsoft.Jet.OLEDB.4.0;Data Source=Database.mdb";
	OleDbConnection^ dbConnection = gcnew OleDbConnection(connectionString);

	dbConnection->Open();
	String^ query = "DELETE FROM [table_name] WHERE id=" + id;
	OleDbCommand^dbComand = gcnew OleDbCommand(query, dbConnection);
	OleDbDataReader^ dbReader = dbComand->ExecuteReader();


	if (dbComand->ExecuteNonQuery() != 1)
		MessageBox::Show("");
	else
		MessageBox::Show("");

	dbConnection->Close();

	return System::Void();


}
