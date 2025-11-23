#include <iostream>
#include <cmath>
using namespace std;

int main() {
    int n;
    cout << "n = ";
    cin >> n;

    // Coordonatele maxim 10 triunghiuri
    double Ax[10], Ay[10];
    double Bx[10], By[10];
    double Cx[10], Cy[10];
    double aria[10];

    for(int i = 0; i < n; i++) {
        cout << "\nTriunghiul " << i+1 << ":\n";
        cin >> Ax[i] >> Ay[i];
        cin >> Bx[i] >> By[i];
        cin >> Cx[i] >> Cy[i];

        // Lungimi laturi
        double a = sqrt((Ax[i] - Bx[i])*(Ax[i] - Bx[i]) + (Ay[i] - By[i])*(Ay[i] - By[i]));
        double b = sqrt((Bx[i] - Cx[i])*(Bx[i] - Cx[i]) + (By[i] - Cy[i])*(By[i] - Cy[i]));
        double c = sqrt((Cx[i] - Ax[i])*(Cx[i] - Ax[i]) + (Cy[i] - Ay[i])*(Cy[i] - Ay[i]));

        double p = (a + b + c) / 2;
        aria[i] = sqrt(p * (p - a) * (p - b) * (p - c));
    }

    cout << "\nA) Ariile triunghiurilor:\n";
    for(int i = 0; i < n; i++)
        cout << "T" << i+1 << " = " << aria[i] << "\n";

    // Gasirea maximului si minimului
    int imax = 0, imin = 0;
    for(int i = 1; i < n; i++) {
        if(aria[i] > aria[imax]) imax = i;
        if(aria[i] < aria[imin]) imin = i;
    }

    cout << "\nB) Triunghiul cu aria maxima este T" << imax+1 << ":\n";
    cout << Ax[imax] << " " << Ay[imax] << "   "
         << Bx[imax] << " " << By[imax] << "   "
         << Cx[imax] << " " << Cy[imax] << "\n";

    cout << "\nC) Triunghiul cu aria minima este T" << imin+1 << ":\n";
    cout << Ax[imin] << " " << Ay[imin] << "   "
         << Bx[imin] << " " << By[imin] << "   "
         << Cx[imin] << " " << Cy[imin] << "\n";

    // D) Afisare triunghiuri in ordine crescatoare a ariilor FARA sortare
    cout << "\nD) Triunghiurile in ordine crescatoare a ariilor:\n";

    // Afisam ariile de la cea mai mica la cea mai mare prin cautare repetata
    bool folosit[10] = {0};
    for(int k = 0; k < n; k++) {
        int poz = -1;
        for(int i = 0; i < n; i++) {
            if(!folosit[i] && (poz == -1 || aria[i] < aria[poz])) {
                poz = i;
            }
        }
        folosit[poz] = true;
        cout << "Aria = " << aria[poz] << " -> ";
        cout << Ax[poz] << " " << Ay[poz] << "   "
             << Bx[poz] << " " << By[poz] << "   "
             << Cx[poz] << " " << Cy[poz] << "\n";
    }

    return 0;
}
