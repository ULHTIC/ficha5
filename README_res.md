**UNIVERSIDADE LUSÓFONA DE HUMANIDADES E TECNOLOGIAS**


# Ficha de Exercícios - 5: Apontadores

Na resolução destes exercícios deve ser utilizada a Linguagem de Programação C. Para além da correta implementação dos requisitos, tenha em conta os seguintes aspetos:

- O código apresentado deve ser bem indentado. 
- O código deve compilar sem erros ou *warnings* utilizando o *gcc* com as seguintes flags:
- `gcc -Wall -Wextra -Wpedantic -std=c99 -g exercicio1.c -o exercicio1`
- Tenha em atenção os nomes dados das variáveis, para que sejam indicadores daquilo que as mesmas vão conter.
- Evite o uso de constantes mágicas. 
- Evite duplicação de código. 
- Considere a implementação de funções para melhorar a legibilidade, evitar a duplicação e criar soluções mais genéricas.


1. Considere a seguinte sequência de instruções:
    ```C
	int var1 ;
	int var2 = 15;
	int * ptr = & var1 ;
	int * ptr2 = ptr;
	*ptr = var2 ;
    ```
   Complete a tabela em baixo preenchendo o conteúdo das variáveis var1, ptr e ptr2 no fim da execuçãao da sequência de instruções. Preencha também o endereço correspondente à variável var2 assumindo que este é o próximo endereço livre possível.
   

	| Endereço | Conteúdo | Identificador |
	|:--------:|:--------:|:-------------:|
	|    ...   |          |               |
	|  0xFF8B4 |          |      var1     |
	|          |    15    |      var2     |
	|    ...   |          |               |
	|  0xFF900 |          |      ptr      |
	|  0xFF908 |          |      ptr2     |
	|    ...   |          |               |



	**Resolução**

	| Endereço | Conteúdo | Identificador |
	|:--------:|:--------:|:-------------:|
	|    ...   |          |               |
	|  0xFF8B4 |    15    |      var1     |
	|  0xFF8B8 |    15    |      var2     |
	|    ...   |          |               |
	|  0xFF900 | 0xFF8B4  |      ptr      |
	|  0xFF908 | 0xFF8B4  |      ptr2     |
	|    ...   |          |               |


	[Resolução no Pythontutor para executar e visualizar passo a passo o que se passa](http://pythontutor.com/c.html#code=int%20main%20%28%29%20%0A%7B%20%0A%20%20int%20var1%20%3B%0A%20%20int%20var2%20%3D%2015%3B%0A%20%20int%20*%20ptr%20%3D%20%26%20var1%20%3B%0A%20%20int%20*%20ptr2%20%3D%20ptr%3B%0A%20%20*ptr%20%3D%20var2%20%3B%0A%7D&curInstr=0&mode=display&origin=opt-frontend.js&py=c_gcc9.3.0&rawInputLstJSON=%5B%5D)


2. Implemente um programa que contenha duas variáveis x e y do tipo int e float, ambas inicializadas com o valor 5. Declare também dois apontadores px e py, que apontam para x e y respetivamente.

	Em seguida mostre o valor das variáveis e o seu endereço armazenado no respetivo apontador. Depois mostre o valor das mesmas variáveis incrementado em uma unidade.
	
	*Notas:*
	Transforme os endereços num long int para melhor compreensão dos resultados.


	**Resolução**

	``` bash C
	int main () 
	{ 
	   int x = 5;
	   float y = 5.0;

	   int *px = &x;
	   float *py = &y;

	   printf("x = %d\n", x);
	   printf("*px = %d\n", *px);
	   printf("px (com %%d) = %d\n", px);
	   printf("px (com %%ld) = %ld\n\n", px);

	   printf("y = %f\n", y);
	   printf("*py = %f\n", *py);
	   printf("%ld\n", py);
	}
	```

	[Resolução no Pythontutor para executar e visualizar passo a passo o que se passa](http://pythontutor.com/c.html#code=int%20main%20%28%29%20%0A%7B%20%0A%20%20%20int%20x%20%3D%205%3B%0A%20%20%20float%20y%20%3D%205.0%3B%0A%20%20%20%0A%20%20%20int%20*px%20%3D%20%26x%3B%0A%20%20%20float%20*py%20%3D%20%26y%3B%0A%20%20%20%0A%20%20%20printf%28%22x%20%3D%20%25d%5Cn%22,%20x%29%3B%0A%20%20%20printf%28%22*px%20%3D%20%25d%5Cn%22,%20*px%29%3B%0A%20%20%20printf%28%22px%20%28com%20%25%25d%29%20%3D%20%25d%5Cn%22,%20px%29%3B%0A%20%20%20printf%28%22px%20%28com%20%25%25ld%29%20%3D%20%25ld%5Cn%5Cn%22,%20px%29%3B%0A%20%20%20%0A%20%20%20printf%28%22y%20%3D%20%25f%5Cn%22,%20y%29%3B%0A%20%20%20printf%28%22*py%20%3D%20%25f%5Cn%22,%20*py%29%3B%0A%20%20%20printf%28%22%25ld%5Cn%22,%20py%29%3B%0A%0A%20%20%20%0A%7D&curInstr=12&mode=display&origin=opt-frontend.js&py=c_gcc9.3.0&rawInputLstJSON=%5B%5D)


3. Qual o valor das variáveis x, y e z no fim da execução do programa?

    ```C
	#include <stdio.h>
	void func(int n, int * a, int * b)
	{
	   n = *a;
	   *a = *b;
	   *b = n++;
	}
	int main(void)
	{
	   int x = 10, y = 15, z = 5;
	   func(z, &x, &y);
	   printf("x = %d, y = %d, z = %d\n", x, y, z);
	   return 0;
	}
    ```
 
	**Resolução**

	x = 15, y=10, z=5

	[Resolução no Pythontutor para executar e visualizar passo a passo o que se passa](http://pythontutor.com/c.html#code=%20%20%20%20%23include%20%3Cstdio.h%3E%0A%20%20%20%20void%20func%28int%20n,%20int%20*%20a,%20int%20*%20b%29%0A%20%20%20%20%7B%0A%20%20%20%20%20%20%20n%20%3D%20*a%3B%0A%20%20%20%20%20%20%20*a%20%3D%20*b%3B%0A%20%20%20%20%20%20%20*b%20%3D%20n%2B%2B%3B%0A%20%20%20%20%7D%0A%20%20%20%20int%20main%28void%29%0A%20%20%20%20%7B%0A%20%20%20%20%20%20%20int%20x%20%3D%2010,%20y%20%3D%2015,%20z%20%3D%205%3B%0A%20%20%20%20%20%20%20func%28z,%20%26x,%20%26y%29%3B%0A%20%20%20%20%20%20%20printf%28%22x%20%3D%20%25d,%20y%20%3D%20%25d,%20z%20%3D%20%25d%5Cn%22,%20x,%20y,%20z%29%3B%0A%20%20%20%20%20%20%20return%200%3B%0A%20%20%20%20%7D&curInstr=11&mode=display&origin=opt-frontend.js&py=c_gcc9.3.0&rawInputLstJSON=%5B%5D)


4. Considere o seguinte código:
    ```C
    int main (int argc, char * argv[]) {
      int numero = 10;  
      int * pNum = NULL;    
      return 0;  
    }    

    ```
    Altere o código para:
    
    a) O ponteiro pNum ficar a apontar para a variável número;
    
    b) Apresente no ecrã o valor da variável número, sem a usar diretamente (ou seja, usando o ponteiro pNum;
    
    c) Altere (por ex. para 15) o valor da variável número sem a usar diretamente (ou seja, usando o ponteiro pNum);
    
    d) Apresente novamente no ecrã o valor da variável número, usando o ponteiro pNum;


	**Resolução**

	``` bash C
	int main (int argc, char * argv[]) {
	  int numero = 10;  
	  int * pNum = &numero;  

	  printf("%d", *pNum);
	  *pNum = 15;
	  printf("%d", *pNum);

	  return 0;  
	} 
	```
	[Resolução no Pythontutor para executar e visualizar passo a passo o que se passa](http://pythontutor.com/c.html#code=int%20main%20%28%29%20%7B%0A%20%20int%20numero%20%3D%2010%3B%0A%20%20int%20*pNum%20%3D%20%26numero%3B%0A%20%20%0A%20%20printf%28%22%25d%22,%20*pNum%29%3B%0A%20%20*pNum%20%3D%2015%3B%0A%20%20printf%28%22%25d%22,%20*pNum%29%3B%0A%20%20%0A%20%20return%200%3B%0A%7D&curInstr=0&mode=display&origin=opt-frontend.js&py=c_gcc9.3.0&rawInputLstJSON=%5B%5D)


5. Considere as funções main () e calcular_dados() que se seguem:
    ```C
	void calcular_dados (...){ //TODO }

	int main() {
	  int x = 10, y = 15;
	  int soma;
	  float media;

	  calcular_dados(...); // TODO
	  printf("Soma = %d\n", soma);
	  printf("Media = %f", media);
	  return 0;
	}
    ```
    
    O objetivo do exercício é implementar a função calcular_dados(...) de maneira a que possa ser usada para calcular a soma e a média de dois números.   
 	Restrições:    
    - A única linha da função main () que pode alterar é a linha da chamada à função  calcular_dados () .    
    -	O cálculo da soma e da média dos dois valores tem obrigatóriamente de ser feito  usando a função calcular_dados  ()
    - Não pode alterar o tipo de retorno da função calcular_dados  ()
    - Não pode usar variáveis globais para resolver este exercício. 


	**Resolução**
	```C
	void calcular_dados (int x, int y, int* pSoma, float* pMedia){
	    *pSoma = x+y;
	    *pMedia = (x+y)/2.0;
	}


	int main() {
	  int x = 10, y = 15;
	  int soma;
	  float media;

	  calcular_dados(x, y, &soma, &media);
	  printf("Soma = %d\n", soma);
	  printf("Media = %f", media);
	  return 0;
	}
	```
	[Resolução no Pythontutor para executar e visualizar passo a passo o que se passa](http://pythontutor.com/c.html#code=void%20calcular_dados%20%28int%20x,%20int%20y,%20int*%20pSoma,%20float*%20pMedia%29%7B%0A%20%20%20%20*pSoma%20%3D%20x%2By%3B%0A%20%20%20%20*pMedia%20%3D%20%28x%2By%29/2.0%3B%0A%7D%0A%0A%0Aint%20main%28%29%20%7B%0A%20%20int%20x%20%3D%2010,%20y%20%3D%2015%3B%0A%20%20int%20soma%3B%0A%20%20float%20media%3B%0A%20%20%0A%20%20calcular_dados%28x,%20y,%20%26soma,%20%26media%29%3B%0A%20%20printf%28%22Soma%20%3D%20%25d%5Cn%22,%20soma%29%3B%0A%20%20printf%28%22Media%20%3D%20%25f%22,%20media%29%3B%0A%20%20return%200%3B%0A%7D&curInstr=0&mode=display&origin=opt-frontend.js&py=c_gcc9.3.0&rawInputLstJSON=%5B%5D)


6.	Implemente uma função que receba uma string  (char *)  e devolva o endereço da  primeira vogal que existe nessa string. Caso não exista nenhuma vogal a função deve devolver  NULL.

    Sugere-se que a função tenha o seguinte protocolo:    
    ```C
    char *primeiraVogal (char *str) {  ...  }
    ``` 
    
	**Resolução** 
	```C 
	    char* primeiraVogal (char *str) {

		while (*str!='\0') {
		if(*str=='a'||*str=='e'||*str=='i'
		   ||*str=='o'||*str=='u'){
		    return str;
		}
		str++;
		}
		return 0;
	    }

	    int main() {

	      char palavra[] = "programa";
	      char *letra;

	      letra = primeiraVogal(palavra);
	      if (letra == 0)
		  printf("'%s' nao tem vogais", palavra);

	      printf("Primeira vogal de '%s': %c", palavra, *letra);
	      return 0;  
	    }
	```
	
	[Resolução no Pythontutor para executar e visualizar passo a passo o que se passa](http://pythontutor.com/c.html#code=%20%20%20%20%0A%20%20%20%20char*%20primeiraVogal%20%28char%20*str%29%20%7B%0A%0A%20%20%20%20%20%20%20%20while%20%28*str!%3D'%5C0'%29%20%7B%0A%20%20%20%20%20%20%20%20if%28*str%3D%3D'a'%7C%7C*str%3D%3D'e'%7C%7C*str%3D%3D'i'%0A%20%20%20%20%20%20%20%20%20%20%20%7C%7C*str%3D%3D'o'%7C%7C*str%3D%3D'u'%29%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20return%20str%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20str%2B%2B%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20return%200%3B%0A%20%20%20%20%7D%0A%20%20%20%20%0A%20%20%20%20int%20main%28%29%20%7B%0A%20%20%20%20%20%20%0A%20%20%20%20%20%20char%20palavra%5B%5D%20%3D%20%22programa%22%3B%0A%20%20%20%20%20%20char%20*letra%3B%0A%20%20%20%20%20%20%0A%20%20%20%20%20%20letra%20%3D%20primeiraVogal%28palavra%29%3B%0A%20%20%20%20%20%20if%20%28letra%20%3D%3D%200%29%0A%20%20%20%20%20%20%20%20%20%20printf%28%22'%25s'%20nao%20tem%20vogais%22,%20palavra%29%3B%0A%20%20%20%20%20%20%0A%20%20%20%20%20%20printf%28%22Primeira%20vogal%20de%20'%25s'%3A%20%25c%22,%20palavra,%20*letra%29%3B%0A%20%20%20%20%20%20return%200%3B%20%20%0A%20%20%20%20%7D&curInstr=21&mode=display&origin=opt-frontend.js&py=c&rawInputLstJSON=%5B%5D)
	

**##################### Exercicios por organizar ##############################**

1.	Crie a declaração apropriada para as seguintes variáveis. Inicialize todos os vetores.
    
    a)	nome é uma cadeia com 10 caracteres
    
    b)	psa é um vetor de 10 ponteiros para caracteres
    
    c)	pstr é um ponteiro para um vetor de 10 caracteres

```C
    char nome[10];
    char* psa[10];
    char* pstr = *psa;
```

2.	Considere as seguintes declarações e responda às questões justificando:

    ```C
    int * ptr;
    int ref[] = {1,2,3,4};
    ptr = &ref[0];
    ```
    a) ref é o endereço de quê?
    
    b) E ref+1?  
    
    c) Qual o valor de *ptr e *(ptr+2) ?

```
a) ref é o endereço de memória da primeira posição do vetor    
b) ref+1 é o endereço de memória da segunda posição do vetor
c) O valor de *ptr é 1 e o valor de *(ptr+2) é 3
```
3.	Considere o seguinte código:
    ```C
    int main (int argc, char * argv[]) {
      int numero = 10;  
      int * pNum = NULL;    
      return 0;  
    }    

    ```
    Altere o código para:
    
    a) O ponteiro pNum ficar a apontar para a variável número;
    
    b) Apresente no ecrã o valor da variável número, sem a usar diretamente (ou seja, usando o ponteiro pNum;
    
    c) Altere (por ex. para 15) o valor da variável número sem a usar diretamente (ou seja, usando o ponteiro pNum);
    
    d) Apresente novamente no ecrã o valor da variável número, usando o ponteiro pNum;

```C
    int numero = 10;
    int * pNum = &numero;//a)
    printf("O valor da variável numero é: %d\n",*pNum);//b)
    *pNum = 15;//c)
    printf("O valor da variável numero é: %d\n",*pNum);//d)
```

4.	Indique justificando qual o output do seguinte código sem o executar:

    a)
    ```C
    int main () {
      int numeros[] = {10, 20, 30};
      int * pNum = &numeros[0];
      printf("Valor = %d\n", *pNum);  
      pNum++;  
      printf("Valor = %d\n", *pNum);  
      pNum = pNum + 1;  
      printf("numero via ponteiro = %d\n", *pNum);  
      return 0; 
    }    
    ```
    b)
    ```C
    #include <stdio.h>   
    #define MAX 5    
    int main () {    
      int numeros[MAX] = {10, 20, 30, 40, 50};    
      int* pNum = numeros;      
      while(pNum<=&numeros[MAX¬-1]) {      
        printf("numero via ponteiro = %d\n", *pNum);      
        pNum++;    
      }      
      return 0;  
    } 
    ```
    
 

7.	Implemente uma função que seja capaz de determinar qual o maior e menor valores de um vetor de inteiros. A função deve respeitar a seguinte assinatura:
    ```C
    void calcMinimoEMaximo (int numeros[], int tamanho, int *min, int *max ) {  }
    ```
    Os valores do menor e maior números devem ser guardados nas posições de memória para as  quais apontem os parâmetros min e max  (ponteiros)  que a função recebe.

```C
void calcMinimoEMaximo (int numeros[], int tamanho, int *min, int *max ) {
    int i = 0;
    for(i=0;i<tamanho;i++){
        if (numeros[i] < *min){
            *min = numeros[i];
        }
        if (numeros[i] > *max){
            *max = numeros[i];
        }
    }
}
```

8.	Considere o array argv[], que faz parte da assinatura standard da função main,  e que permite receber argumentos de linha de comandos, durante a execução do programa.
    ```C
    int main (int argc, char* argv[]) { 
 		  /* … */  
      return 0;  
    }
    ```
    
    O parâmetro argc tem o número de argumentos e o parâmetro argv[] tem os valores dos argumentos.
    Implemente um programa que seja capaz de obter valores indeterminados como argumentos de linha de comandos. O programa deve listar os vários argumentos, precedidos de um prefixo numérico, que deve começar em 1. Caso não seja fornecido nenhum argumento, o programa deve apresentar uma mensagem indicativa.

    Seguem-se três exemplos de sessões do programa:
    ```bash
    > nome¬programa.exe
    Não foram introduzidos argumentos.
    > nome¬programa.exe ola  
    Os argumentos são:  1 ¬ ola    
    > nome¬programa.exe ola ole  
    Os argumentos são:  1 ¬ ola  2 ¬ ole
    ```
    *Notas:*
    - Tenha em conta que argv[0] irá conter o nome do programa. Esse argumento não deverá aparecer no seu output.

```C
#include <stdio.h>

int main( int argc, char* argv[] ) // argv Ã© um vetor de strings
{
    int i;

    if(argc == 1)
    {
        printf("Nao existem argumentos.\n");
    }    
    else
    {
        printf("Os argumentos sao: ");

        for(i=1; i<argc; ++i)
            printf("%d %s ", i, argv[i]);

        printf("\n\n");  
    }
    return 0;
}
```

9.	Seja o seguinte trecho de programa:
    ```C
    int i=3,j=5;
    int *p, *q;
    p = &i;
    q = &j;
    ```
    Qual é o valor das seguintes expressões ?
	  
    a) p == &i;
    
    b) *p - *q
    
    c) **&p
    
    d) 3* - *p/(*q)+7


10.	Qual será a saída deste programa supondo que i ocupa o endereço 4094 na memória?
    ```C
    main() {
      int i=5, *p;
      p = &i;
      printf(“%ld %d %d %d %d\n”, (long)p,*p+2,**&p,3**p,**&p+4);
    }
    ```

11.	Se i e j são variáveis inteiras e p e q ponteiros para int, quais das seguintes expressões de atribuição são ilegais?
      
      a.	p = &i;
      
      b.	*q = &j;
      
      c.	p = &*&i;
      
      d.	i = (*&)j;
      
      e.	i = *&j;
      
      f.	i = *&*&j;
      
      g.	q = *p;
      
      h.	i = (*p)++ + *q


12.	Qual é o resultado do seguinte programa?
    ```C
    #include <conio.h>
    #include <stdio.h>
    void main(){
      float vet[5] = {1.1,2.2,3.3,4.4,5.5};
      float *f;
      int i;
      f = vet;
      printf("contador/valor/valor/endereco/endereco");
      for(i = 0 ; i <= 4 ; i++){
        printf("\ni = %d",i);
        printf("   vet[%d] = %.1f",i, vet[i]);
        printf("   *(f + %d) = %.1f",i, *(f+i));
        printf("   &vet[%d] = %ld",i, (long)&vet[i]);
        printf("   (f + %d) = %ld",i, (long)f+i);
      }
    }
    ```
13.	Assumindo que pulo[] é um vetor do tipo int, quais das seguintes expressões referenciam o valor do terceiro elemento da matriz?
    
    a.	*(pulo + 2)
    
    b.	*(pulo + 4)
    
    c.	pulo + 4
    
    d.	pulo + 2

14. Supor a declaração: int mat[4], *p, x; Quais expressões são válidas? Justifique:
    
    a.	p = mat + 1;
    
    b.	p = mat++;
    
    c.	p = ++mat;
    
    d.	x = (*mat)++;

15. O que fazem os seguintes programas:
    a)
    ```C
    #include <stdio.h>
    void main(){
      int vet[] = {4,9,13};
      int i;
      for(i=0;i<3;i++){
        printf("%d ",*(vet+i));
      }
    }
    ```
    b)
    ```C
    #include <stdio.h>
    void main(){
      int vet[] = {4,9,13};
      int i;
      for(i=0;i<3;i++){
        printf("%ld ",(long)vet+i);
      }
    }
    ```
    c)
    ```C
    #include <stdio.h>
    void main(){
      int vet[] = {4,9,13};
      int i;
      for(i=0;i<3;i++){
        printf("%d ", ++*(vet+i));
      }
    }
    ```
 16. O que faz o seguinte programa quando executado?
    
    a)    
    ```C
    #include <stdio.h>
    void main() {
      int vet[] = {4,9,12};
      int i,*ptr;
      ptr = vet;
      for(i = 0 ; i < 3 ; i++) {
        printf("%d ",*ptr++);
      }
    }
    ```
    b)
    ```C
    #include <stdio.h>
    void main(){
      int vet[] = {4,9,12};
      int i,*ptr;
      ptr = vet;
      for(i = 0 ; i < 3 ; i++) {
        printf("%d ",(*ptr)++);
      }
    }
    ```

17.	Seja vet um vetor de 4 elementos: TIPO vet[4]. Supor que depois da declaração, vet esteja armazenado no endereço de memória 4092 (ou seja, o endereço de vet[0]). Supor também que na máquina usada uma variável do tipo char ocupa 1 byte, do tipo int ocupa 2 bytes, do tipo float ocupa 4 bytes e do tipo double ocupa 8 bytes.

  Qual o valor de vet+1, vet+2 e vet+3 se:
  
    a.	vet for declarado como char?
    
    b.	vet for declarado como int?
    
    c.	vet for declarado como float?
    
    d.	vet for declarado como double?
    
   
