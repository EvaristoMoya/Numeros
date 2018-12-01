#include <iostream>
#include <algorithm>
#include <fstream>
#include <string>
#include <vector>
#include <cmath>

using namespace std;

//Función para calcular la moda

void mode(vector<float> new_array, int num)
{
    int* ipRepetition = new int[num];

    for (int i = 0; i < num; i++) {
        ipRepetition[i] = 0;
        int j = 0;//
        while ((j < i) && (new_array[i] != new_array[j])) {
            if (new_array[i] != new_array[j]) {
                j++;
            }
        }
        (ipRepetition[j])++;
    }
    int iMaxRepeat = 0;
    for (int i = 1; i < num; i++) {
        if (ipRepetition[i] > ipRepetition[iMaxRepeat]) {
            iMaxRepeat = i;
        }
    }

    if(iMaxRepeat==0)
    {
        cout << "No hay moda" << endl << endl;
    }
    else
        cout << "La moda es " << new_array[iMaxRepeat] << endl << endl;
}

int main()
{
    ifstream texto("numeros.txt");

    string linea;
    float numero;

    long double sumaTotal=0;
    int numeroLineas = 0;
    float media;
    vector<float> arregloNumeros;
    float sumaVarianza=0;
    float varianzaMuestral;
    float varianzaPoblacional;

    if(texto.is_open())
    {
        while(getline(texto,linea))
        {
            ++numeroLineas;
            replace(linea.begin(),linea.end(),',','.');
            numero=strtof((linea).c_str(),0);
            sumaTotal+=numero;
            cout << numero << endl; //muestra los números
            arregloNumeros.push_back(numero);
        }

        cout << "La suma total es " << sumaTotal << endl << endl;
        cout << "La cantidad de elementos es " << numeroLineas << endl << endl;
        media = sumaTotal/numeroLineas;
        cout << "La media es " << media << endl << endl;
        sort(arregloNumeros.begin(),arregloNumeros.end());
        if(numeroLineas%2==0)
        {
            cout << "Las mediana es " << (arregloNumeros[(numeroLineas-1)/2]+arregloNumeros[(numeroLineas)/2])/2 << endl << endl;
        }

        else
            cout << "La mediana es " << arregloNumeros[numeroLineas/2] << endl << endl;

        //mode(arregloNumeros,numeroLineas);

        for(int i=0;i<numeroLineas;i++)
        {
            sumaVarianza=sumaVarianza+pow(arregloNumeros[i]-media,2);
        }


        varianzaMuestral=sumaVarianza/(numeroLineas-1);
        varianzaPoblacional=sumaVarianza/(numeroLineas);

        cout << "La desviaci\242n est\240ndar muestral es " << sqrt(varianzaMuestral) << endl << endl;
        cout << "La desviaci\242n est\240ndar poblacional es " << sqrt(varianzaPoblacional) << endl << endl;

        texto.close();
    }

    else
        cout << "No se encuentra archivo" << endl;

    return 0;
}
