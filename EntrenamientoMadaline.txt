%Creditos 06/10/2018
%Docente: Angel Gabriel Diaz Maza
%Compañero: Duvan Restrepo Uribe
%Yo: William Murillo Mena 
%Madaline, 3 entradas y 5 neuronas

%Matriz con las entradas
x=[0 0 0 0 1 1 1 1;0 0 1 1 0 0 1 1;0 1 0 1 0 1 0 1];

%Matriz con valores deseados
dx= [0 1 2 3 4 5 6 7];

%Factor de aprendizaje
alfa=0.2;

%Ciclo para llenar la matriz con pesos
%Dimensión de la matriz w[5,3]

for i=1:5 % Ciclo para controlar las filas, una fila para cada neurona
   for j=1:3 %Ciclo para controlar las columnas, pesos de cada entrada
       w(i, j)=rand();
   end
end 

%Ciclo para llenar con 0s la matriz con los valores de salida
%Dimensión de la matriz y[5,8]

for i=1:5 %Ciclo para controlar filas, salida de cada neurona
        for j=1:8 % ciclo para control de columnas, subindice de salidas
    
        y(i,j)=0;
        end
end

%Cantidad de epocas
epocas=10000;

n=0;


%Ciclo para controlar las epocas
while(n<epocas)

%Ciclo para llenar con 0s el vector con los errores de cada neurona
    for i=1:5
        error(i)=0;
    end
    
%Ciclo para llenar con 0s la matriz de Y de salidas
for i=1:5 %salidas
        for j=1:8 % las 8 opciones de salida
        y(i,j)=0;
        end
end

%Inicialización de valor
    h=1;
    
%Ciclo para recorrer las columnas
    while(h<9)
      
        cad=0;
      
        %Ciclo para controlar filas de la matriz Y(salidas) & matriz W (Pesos)
        %
        
        for i=1:5
       
           %Ciclo para controlar las columnas de la matriz W
             % y para controlar las filas de la matriz x
         for j=1:3 
          
          
          %Se calcula la salida
                 y(i,h)=y(i,h)+w(i,j)*x(j,h);
        
         end
         
         %Se calcula el error 
         error(i)=error(i)+0.5*(y(i,h)-dx(h))^2;
         
         %acumulando el error de las cinco neuronas en la primera salida
         %Si la neurona 1 en la 1era salida genera error cad aumenta
         %Si la neurona 2 en la 1era salida genera error cad aumento
         %Si la neurona 3 en la 1era salida no genera error cad no aumento
         %...
         %Hasta: Si la neurona 5 en la 8 salida.
         
         %y así con cada deseado para cada salida de las 5 neuronas
         %Esto sirve para poder decir: (Si al menos 3 neuronas están dentro del error admitido, continuar con el calculo del siguiente deseado para cada salida de las 5 neuronas)
         
         
         if error(i)>0.00001
            
             cad=cad+1;
             
         end
        end
        
        %Si al menos 3 salidas de las 5 neuronas, para el deseado n
        %cumplen con el error, se admiten los pesos y se aumenta el valor de la columna en Y  
        %Para proceder a calcular las salidas y obtener el siguiente deseado
        if cad<3
        
        %Se aumenta el valor de la matriz Y
            h=h+1;
            
            %Comprueba si no existen mas columnas y termina la ejecución
            if h==9
                n=epocas;
            end
            
        else % Actualización de pesos
           for i=1:5 %Ciclo para controlar las filas de la matriz W 
               for j=1:3 %Ciclo para controlar las columnas de las matriz W
               
                    w(i,j) = w(i,j)+alfa*(dx(h)-y(i,h))*x(j,h);
               end
           end  
           
           %Se iguala, para que salga inicie los calculos desde la primera
           %Fila de Y
            h=9;
            
        end
        
    end
    
    %Aumento de epocas
    n=n+1;
end

y
w

epocas