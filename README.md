# Calculadora de Área de Paralelogramo (Via Vetores)

Este projeto é uma calculadora de área de um paralelogramo que utiliza vetores para calcular a área. O código foi desenvolvido utilizando Python, NumPy e a biblioteca Rich para exibir resultados de forma estilizada.

## Funcionalidades

*   **Cálculo da Área:** Calcula a área do paralelogramo com base nos componentes dos dois vetores que o formam.
*   **Solicitação de Entrada do Usuário:** Permite que o usuário insira os componentes dos vetores X e Y.
*   **Tratamento de Erros:**  Valida a entrada do usuário, garantindo que sejam números, e fornece mensagens de erro claras em caso de entrada inválida.
*   **Exibição de Resultados:**  Exibe os vetores inseridos pelo usuário e a área calculada de forma organizada e formatada, utilizando a biblioteca Rich para melhorar a experiência do usuário.
*   **Verificação de Colinearidade:** Detecta se os vetores são colineares (paralelos) e exibe uma mensagem informativa se for o caso.

## Pré-requisitos

*   **Python:**  Versão 3.6 ou superior.
*   **NumPy:**  Necessário para realizar operações matemáticas com vetores.  Instale com: `pip install numpy`
*   **Rich:**  Biblioteca para criar interfaces de usuário textuais mais ricas e coloridas.  Instale com: `pip install rich`

## Como Executar o Código

1.  Salve o código em um arquivo Python (por exemplo, `calculadora_paralelogramo.py`).
2.  Abra um terminal ou prompt de comando.
3.  Navegue até o diretório onde você salvou o arquivo.
4.  Execute o script com o comando: `python calculadora_paralelogramo.py`

## Código Fonte

```python
import numpy as np
from rich.console import Console
from rich.table import Table


#instalar o pip install numpy rich

console = Console()

def calcular_area_paralelogramo(vetor1, vetor2):
    """Calcula a área do paralelogramo usando o determinante."""
    matriz = np.array([vetor1, vetor2])
    determinante = np.linalg.det(matriz)
    return abs(determinante)

def obter_vetor(nome_vetor):
    """solicita os componentes de um vetor ao usuário."""
    console.print(f"\n[bold blue]Configurando {nome_vetor}:[/bold blue]")
    while True:
        try:
            x = float(input(f" Componente X: "))
            y = float(input(f" Componente Y: "))
            return np.array([x, y])
        except ValueError:
            console.print("[red]Entrada inválida! Digite apenas números.[/red]")

def main():
    console.clear()
    console.print("[bold green]Calculadora de Área de Paralelogramo (Via Vetores)[/bold green]")
    console.print("---" * 15)

    try:
        # Coleta de dados
        v1 = obter_vetor("Vetor 1")
        v2 = obter_vetor("Vetor 2")

        # Cálculo
        area = calcular_area_paralelogramo(v1, v2)

        # exibição estilizada com Rich
        table = Table(title="\nResultado do Cálculo", header_style="bold magenta")
        table.add_column("Vetor", justify="center")
        table.add_column("Componente X", justify="center")
        table.add_column("Componente Y", justify="center")
        
        table.add_row("Vetor 1", f"{v1[0]:.2f}", f"{v1[1]:.2f}")
        table.add_row("Vetor 2", f"{v2[0]:.2f}", f"{v2[1]:.2f}")
        
        console.print(table)
        
        # resultado final
        if area == 0:
            console.print(f"\n[yellow]Área: {area:.2f}[/yellow]")
            console.print("[italic]Nota: Os vetores são colineares, por isso a área é zero.[/italic]")
        else:
            console.print(f"\n[bold green]Área Total: {area:.4f} unidades de área.[/bold green]")

    except Exception as e:
        console.print(f"[red]Ocorreu um erro inesperado: {e}[/red]")

if __name__ == "__main__":
    main()
