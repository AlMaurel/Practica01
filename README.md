#include <iostream>
#include <string>
using namespace std;

int solicitaAnyo();
int solicitaMes();
int solicitaDia(int mesInt, int anyoInt);
bool esBisiesto(int anyoInt);
int diasMes(int mesInt, int anyoInt);
int contarBisiestos(int anyoInicio, int anyoInt);
long int diasAnyosCompletos(int anyo);
int diasEsteAnyo(int diaInt, int mesInt, int anyoActual);
long int diasTranscurridos(int diaFinal, int mesIntroducido, int anyoActual);
int diaSemana(long int numDias);
string nombreDia(int representacionDia);
int funcion1();
int menu();
int primerDomingoMes(int mes, int anyo);

int main() 
{
	int operacion;
	operacion = menu();
	cout << operacion;

	return 0;
}

/* POR COMPLETAR
Esta función permite al usuario elegir entre una de las 4 funcionalidades de la versión 2, además de cerrar el programa.*/
int menu()
{
	int opcion, operacion;
	cout << "Elija una opción: " << endl;
	cout << "1 - Calcular el día de la semana para una fecha dada" << endl;
	cout << "2 - Obtener la fecha correspondiente al primer domingo de un año" << endl;
	cout << "3 - Obtener los domingos de un año" << endl;
	cout << "4 - Obtener los posibles puentes de un año" << endl;
	cout << "0 - Salir" << endl;
	cin >> opcion;

	while (opcion < 0 || opcion > 4)
	{
		cout << "Opción no válida. Por favor, elija una de las funciones anteriores." << endl;
		cin >> opcion;
	}
	
	if (opcion == 1)
	{
		operacion = funcion1();
	}
	else if (opcion == 2)
	{
		int anyoUsuario;
		cout << "Introduzca un año" << endl;
		cin >> anyoUsuario;
		operacion = primerDomingoMes(1, anyoUsuario);
	}
	
	return operacion;
}

int primerDomingoMes(int mes, int anyo)
{
	int anyoIntroducido, mesIntroducido, diaIntroducido, diasTieneElMes, anyosBisiestosHastaLaFecha, diasEsteAny, diaDeSemana;
	long int diasAnyosCompl, diasTotales;
	bool anyoBisiesto;
	int anyoInicio;
	int a = 0;

	anyoBisiesto = esBisiesto(anyo);
	diasTieneElMes = diasMes(mes, anyo);

	diasAnyosCompl = diasAnyosCompletos(anyo);
	diasTotales = diasTranscurridos(a, mes, anyo);

	while (diasTotales % 7 != 0)
	{
		a = a + 1;
		diasTotales = diasTranscurridos(a, mes, anyo);
	}

	return diasTotales;

}

string diaDeLaSemana(int dia, int mes, int anyo)
{
	string fechaEscritaComoCadenaDeCaracteres;

	fechaEscritaComoCadenaDeCaracteres = "string(dia)

	return fechaEscritaComoCadenaDeCaracteres;
}

int funcion1()
{
	int anyoIntroducido, mesIntroducido, diaIntroducido, diasTieneElMes, anyosBisiestosHastaLaFecha, diasEsteAny, diaDeSemana;
	long int diasAnyosCompl, diasTotales;
	bool anyoBisiesto;
	int anyoInicio;
	string diaDeLaSemanaEnLetras;

	anyoIntroducido = solicitaAnyo();
	mesIntroducido = solicitaMes();
	diaIntroducido = solicitaDia(mesIntroducido, anyoIntroducido);
	anyoBisiesto = esBisiesto(anyoIntroducido);
	diasTieneElMes = diasMes(mesIntroducido, anyoIntroducido);

	diasAnyosCompl = diasAnyosCompletos(anyoIntroducido);
	diasEsteAny = diasEsteAnyo(diaIntroducido, mesIntroducido, anyoIntroducido);
	diasTotales = diasTranscurridos(diaIntroducido, mesIntroducido, anyoIntroducido);

	diaDeSemana = diaSemana(diasTotales);
	diaDeLaSemanaEnLetras = nombreDia(diaDeSemana);

	cout << anyoIntroducido << " " << mesIntroducido << " " << diaIntroducido << " " << diasTotales << " " << diaDeLaSemanaEnLetras;
	


	return 0;
}

// Esta función pide un año, lo valida (para que sea posterior a 1900) y lo devuelve.
int solicitaAnyo()
{
	int anyoUsuario;

	// Leeremos por el teclado hasta que recibamos un año mayor o igual a 1900
	cout << "Introduce un año igual o posterior a 1900: ";
	cin >> anyoUsuario;

	while (cin.fail() || anyoUsuario < 1900)
	{
		cin.clear();
		cin.ignore(10000, '\n');
		cout << "Introduce un año igual o posterior a 1900: ";
		cin >> anyoUsuario;
	}
	cin.ignore(10000, '\n');

	return anyoUsuario;
}

int solicitaMes()
{
	int mesUsuario;

	// Leeremos por el teclado hasta que recibamos un mes válido
	cout << "Introduce el número de un mes: ";
	cin >> mesUsuario;
	while (cin.fail() || mesUsuario > 12 || mesUsuario <= 0)
	{
		cin.clear();
		cin.ignore(10000, '\n');
		cout << "Introduce el número de un mes: ";
		cin >> mesUsuario;
	}
	cin.ignore(10000, '\n');
	return mesUsuario;

}

int solicitaDia(int mesInt, int anyoInt)
{
	int diaIntroducido;

	// leeremos por el teclado hasta que recibamos un entero
	cout << "Introduce el número del día: ";
	cin >> diaIntroducido;
	while (cin.fail() || diaIntroducido <= 0 || diaIntroducido > diasMes(mesInt, anyoInt))
	{
		cin.clear();
		cin.ignore(10000, '\n');
		cout << "Introduce el número del día: ";
		cin >> diaIntroducido;
	}
	cin.ignore(10000, '\n');
	return diaIntroducido;
}

bool esBisiesto(int anyoInt)
{

	int resto4, resto100, resto400;
	bool esElAnyoBisiesto;

	resto4 = anyoInt % 4;
	resto100 = anyoInt % 100;
	resto400 = anyoInt % 400;
	if (resto4 != 0)
	{
		esElAnyoBisiesto = false;
	}
	else
	{
		if (resto400 == 0)
		{
			esElAnyoBisiesto = true;
		}
		else
		{
			if (resto100 == 0)
			{
				esElAnyoBisiesto = false;
			}
			else
			{
				esElAnyoBisiesto = true;
			}
		}
	}

	return esElAnyoBisiesto;
}

int diasMes(int mesInt, int anyoInt)
{
	bool anyo_bisiesto;
	anyo_bisiesto = esBisiesto(anyoInt);

	int cuantosDiasTieneElMes;
	if (mesInt == 1 || mesInt == 3 || mesInt == 5 || mesInt == 7 || mesInt == 8 || mesInt == 10 || mesInt == 12)
	{
		cuantosDiasTieneElMes = 31;
	}
	if (mesInt == 4 || mesInt == 6 || mesInt == 9 || mesInt == 11)
	{
		cuantosDiasTieneElMes = 30;
	}
	if (mesInt == 2 && anyo_bisiesto == true)
	{
		cuantosDiasTieneElMes = 29;
	}
	if (mesInt == 2 && anyo_bisiesto == false)
	{
		cuantosDiasTieneElMes = 28;
	}
	return cuantosDiasTieneElMes;
}


/* Esta función cuenta el número de años bisiestos desde el año de inicio hasta el año de 
fin (para nuestro calendario estableceremos el 1900 por defecto y el de fin será el introducido por el usuario) */

int contarBisiestos(int anyoInicio, int anyoFinal)
{

	int a = anyoInicio;
	int numeroAnyosBisiestos = 0;

	/* Hacemos un contador de años bisiestos: si el año es bisiesto (determinado por la función esBisiesto(anyo) 
	se sumará uno a nuestro contador (la variable "numeroAnyosBisiestos") */

	while (a <= anyoFinal)
	{
		if (esBisiesto(a) == true)
		{
			numeroAnyosBisiestos = numeroAnyosBisiestos + 1;
		}

		a = a + 1;

	}

	return numeroAnyosBisiestos;
}

// La función calcula el número de días transcurridos desde el 1/1/1900 hasta el 1/1/anyo

long int diasAnyosCompletos(int anyo)
{
	int anyosTotales, anyosBisiestos, anyosNoBisiestos, diasTotales;

	anyosTotales = anyo - 1900;
	// Clave el anyo - 1 !!!!!!!!!!!
	anyosBisiestos = contarBisiestos(1900, anyo - 1);
	anyosNoBisiestos = anyosTotales - anyosBisiestos;

	diasTotales = anyosBisiestos * 366 + anyosNoBisiestos * 365;

	return diasTotales;
}

int diasEsteAnyo(int diaFinal, int mesIntroducido, int anyoActual)
{
	int a = 1;
	int diasEsteAnyoMeses = 0, diasEsteAnyoTotales;

	//Comenzamos con a en enero y a través del bucle va recorriendo todos los meses hasta el anterior al introducido
	while (a < mesIntroducido)
	{
		int diasEsteMes = diasMes(a, anyoActual);

		diasEsteAnyoMeses = diasEsteAnyoMeses + diasEsteMes;

		a = a + 1;

	}

	diasEsteAnyoTotales = diasEsteAnyoMeses + diaFinal;

	return diasEsteAnyoTotales;
}

long int diasTranscurridos(int diaFinal, int mesIntroducido, int anyoActual)
{
	int diasTotales, diasEsteAnyoMeses, diasTotalesTotales;

	diasEsteAnyoMeses = diasEsteAnyo(diaFinal, mesIntroducido, anyoActual);
	diasTotales = diasAnyosCompletos(anyoActual);
	diasTotalesTotales = diasEsteAnyoMeses + diasTotales;

	return diasTotalesTotales;
}

int diaSemana(long int numDias)
{
	int diaDeLaSemana;
	diaDeLaSemana = (numDias)  % 7;

	return diaDeLaSemana;
}

string nombreDia(int representacionDia)
{
	int numeroDelDia;
	string diaFinal;

	if (representacionDia > 0)
	{
		numeroDelDia = diaSemana(representacionDia) - 1;
	}
	else 
	
		numeroDelDia = diaSemana(representacionDia) + 6;
	

	if (numeroDelDia == 0) 
	{ 
		diaFinal = "Lunes";
	}

	else if (numeroDelDia == 1)
	{
		diaFinal = "Martes";
	}

	else if (numeroDelDia == 2)
	{
		diaFinal = "Miercoles";
	}

	else if (numeroDelDia == 3)
	{
		diaFinal = "Jueves";
	}

	else if (numeroDelDia == 4)
	{
		diaFinal = "Viernes";
	}

	else if (numeroDelDia == 5)
	{
		diaFinal = "Sábado";
	}
	else
	{
		diaFinal = "Domingo";
	}

	return diaFinal;
}
