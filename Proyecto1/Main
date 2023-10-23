#include <iostream>
#include <fstream>
#include <vector>
#include <algorithm>
#include <string>
using namespace std;

struct Linea{
    string mes;
    string dia;
    string a;
    string hora;
    string ip;
    string error;
};

vector<Linea> leerArchivo(const string& filename){
  vector<Linea> vectorAux;
  Linea lineaAux;
  ifstream inputFile(filename);
  while (inputFile >> lineaAux.mes >> lineaAux.dia >> lineaAux.a >> lineaAux.hora >> lineaAux.ip) 
  {
    getline(inputFile, lineaAux.error);
    vectorAux.push_back(lineaAux);
  }
  inputFile.close();
  
  return vectorAux;
}
string mesAValor(string mes){
  string numeroMes;
  if(mes == "Jan"){
  numeroMes = "01";
  
  }
  else if(mes == "Feb"){
    numeroMes = "02";
    
    }
  else if(mes == "Mar"){
    numeroMes = "03";
    }
  else if(mes == "Apr"){
    numeroMes = "04";
    }
  else if(mes == "May"){
    numeroMes = "05";
    }
  else if(mes == "Jun"){
    numeroMes = "06";
    }
  else if(mes == "Jul"){
    numeroMes = "07";
    }
  else if(mes == "Aug"){
    numeroMes = "08";
    }
  else if(mes == "Sep"){
    numeroMes = "09";
    }
  else if(mes == "Oct"){
    numeroMes = "10";
    }
  else if(mes == "Nov"){
    numeroMes = "11";
    }
  else if(mes == "Dec"){
    numeroMes = "12";
    }
  return numeroMes;
}
string valorAMes(string numeroMes) {
  string mes;

  if(numeroMes == "01"){
    mes = "Jan";
  }
  else if(numeroMes == "02"){
    mes = "Feb";
  }
  else if(numeroMes == "03"){
    mes = "Mar";
  }
  else if(numeroMes == "04"){
    mes = "Apr";
  }
  else if(numeroMes == "05"){
    mes = "May";
  }
  else if(numeroMes == "06"){
    mes = "Jun";
  }
  else if(numeroMes == "07"){
    mes = "Jul";
  }
  else if(numeroMes == "08"){
    mes = "Aug";
  }
  else if(numeroMes == "09"){
    mes = "Sep";
  }
  else if(numeroMes == "10"){
    mes = "Oct";
  }
  else if(numeroMes == "11"){
    mes = "Nov";
  }
  else if(numeroMes == "12"){
    mes = "Dec";
  }
  
  return mes;
}
bool comparacionFecha(Linea l1, Linea l2){
  string fecha1= l1.a +"-"+mesAValor(l1.mes)+"-"+l1.dia+" "+l1.hora;
  string fecha2= l2.a +"-"+mesAValor(l2.mes)+"-"+l2.dia+" "+l2.hora;
  
  if(fecha1 <=fecha2){
    
    return true;
    
  }
  else{
    
    return false;
  }
  
}


void merge(vector<Linea> &list, int left, int mid, int right) {
    // Creamos lista izquierda
    vector<Linea> leftList;
    for (int i=left; i<=mid; i++) {
        leftList.push_back(list[i]);
    }
    // Creamos lista derecha
    vector<Linea> rightList;
    for (int j=mid+1; j<=right; j++) {
        rightList.push_back(list[j]);
    }
    // Comparamos mientras haya elementos en las dos listas por comparar
    // crear un índice auxiliar para determinar a donde vamos a mover el valor menor
    int auxIndex = left;
    // Inicializamos los índices para recorrer las dos tablas
    int leftIndex = 0;
    int rightIndex = 0;
    while (leftIndex < leftList.size() && rightIndex < rightList.size()) {
        // Comparamos los valores de la lista izquierda con los de la derecha
        if (comparacionFecha(leftList[leftIndex], rightList[rightIndex])) {
            // El de la izquierda es menor
            list[auxIndex] = leftList[leftIndex];
            // Incremento leftIndex
            leftIndex++;
        } else {
            // El de la derecha es mayor
            list[auxIndex] = rightList[rightIndex];
            // Incremento rightIndex
            rightIndex++;
        }
        // Incremento auxIndex
        auxIndex++;   
    }
    // Vaciamos los valores restantes de la izquierda
    while (leftIndex < leftList.size()) {
        // El de la izquierda es menor
        list[auxIndex] = leftList[leftIndex];
        // Incremento leftIndex
        leftIndex++;
        // Incremento auxIndex
        auxIndex++;
    }
    // Vaciamos los valores restantes de la derecha
    while (rightIndex < rightList.size()) {
        // El de la derecha es mayor
        list[auxIndex] = rightList[rightIndex];
        // Incremento rightIndex
        rightIndex++;
        // Incremento auxIndex
        auxIndex++;
    }
}

void mergeSort(vector<Linea> &list, int left, int right) {
    // Condición de control cuando solo sea un elemento
    if (left < right) {
        // Calculamos el índice del medio
        int mid = left + (right - left) / 2;
        // Ordenamos la lista del lado izquierdo (left->mid)
        mergeSort(list, left, mid);
        // Ordenamos la lista del lado derecho (mid+1 -> right)
        mergeSort(list, mid+1, right);
        // Se realiza el merge para ordenar la lista
        merge(list, left, mid, right);
    }
}

void escribirEnArchivo(const vector<Linea>& vectorOrdenado, const string& archivo) {
    ofstream outputFile(archivo);
    if (!outputFile.is_open()) {
        cerr << "No se pudo abrir el archivo de salida." << endl;
        return;
    }

    for (const Linea& linea : vectorOrdenado) {
        outputFile << linea.mes << " " << linea.dia << " " << linea.a << " " << linea.hora << " " << linea.ip << " " << linea.error << endl;
    }

    outputFile.close();
}

int busquedaBinariaInicio(vector<Linea> vect, Linea fecha) {
    int arriba = vect.size() - 1;
    int abajo = 0;

    while (abajo <= arriba) {
        int medio = abajo + (arriba - abajo) / 2;
        if (comparacionFecha(fecha, vect[medio]) && !comparacionFecha(fecha, vect[medio-1]) ) {
            return medio;
        } else if (comparacionFecha(fecha, vect[medio])) {
            arriba = medio - 1;
        } else {
            abajo = medio + 1;
        }
    }
    return 0;
}

int busquedaBinariaFinal(vector<Linea> vect, Linea fecha) {
    int arriba = vect.size() - 1;
    int abajo = 0;

    while (abajo <= arriba) {
        int medio = abajo + (arriba - abajo) / 2;
        if (comparacionFecha(fecha, vect[medio]) && !comparacionFecha(fecha, vect[medio-1]) ) {
            return medio-1;
        } else if (comparacionFecha(fecha, vect[medio])) {
            arriba = medio - 1;
        } else {
            abajo = medio + 1;
        }
    }
    return 0;
}

void rangoFechas(vector<Linea> vect, Linea linea1, Linea linea2,const string& archivo){
  int indice1=busquedaBinariaInicio(vect,linea1);
  int indice2=busquedaBinariaFinal(vect,linea2);
  ofstream outputFile(archivo);
  if (!outputFile.is_open()) {
        cerr << "No se pudo abrir el archivo de salida." << endl;
        return;
  }

  for(int i=indice1;i<=indice2;i++){
    cout<<vect[i].mes<< " "<<vect[i].dia << " " << vect[i].a << " " << vect[i].hora << " " <<
      vect[i].ip << vect[i].error << endl;
    outputFile<<vect[i].mes<< " "<<vect[i].dia << " " << vect[i].a << " " << vect[i].hora << " " << vect[i].ip << vect[i].error << endl;
  }
  outputFile.close();
}


int main() {
  
  vector<Linea> log = leerArchivo("log608.txt");
  mergeSort(log,0,log.size()-1);
  string mes;
  string hora;
  string minuto;
  string segundo;
  string dia;
  escribirEnArchivo(log, "output608.txt");
  Linea linea1,linea2;
  cout<<"Ingrese valores del rango inicial"<<endl;
  cout<<"Año: ";
  cin>> linea1.a;
  cout<<"Mes (Formato mm ejemplo 02 para el segundo mes): ";
  cin>> mes;
  linea1.mes=valorAMes(mes);
  cout<<"Dia (Formato dd ejemplo 02 para el segundo dia): ";
  cin>> linea1.dia;
  cout<<"Hora(Formato hh ejemplo 05 para las 5AM y 17 para las 5PM): ";
  cin>> hora;
  cout<<"Minuto(Formato mm ejemplo 01 para el primer minuto): ";
  cin>> minuto;
  cout<<"Segundo(Formato ss ejemplo 01 para el primer segundo): ";
  cin>> segundo;
  linea1.hora= hora+":"+"minuto"+":"+segundo;
  linea1.ip="0";
  linea1.ip="NA";
  cout<<"Ingrese valores del rango final"<<endl;
  cout<<"Año: ";
  cin>> linea2.a;
  cout<<"Mes (Formato mm ejemplo 02 para el segundo mes): ";
  cin>> mes;
  linea2.mes=valorAMes(mes);
  cout<<"Dia (Formato dd ejemplo 02 para el segundo dia): ";
  cin>> linea2.dia;
  cout<<"Hora(Formato hh ejemplo 05 para las 5AM y 17 para las 5PM): ";
  cin>> hora;
  cout<<"Minuto(Formato mm ejemplo 01 para el primer minuto): ";
  cin>> minuto;
  cout<<"Segundo(Formato ss ejemplo 01 para el primer segundo): ";
  cin>> segundo;
  linea2.hora= hora+":"+"minuto"+":"+segundo;
  linea2.ip="0";
  linea2.ip="NA";
  rangoFechas(log,linea1,linea2,"range608.txt");
  
}
