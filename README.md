"""CALCULAR-NOTAS-CNU-
Este código é para você adicionar  notas e calcular
Nota 
máxima 
ponderada"""

import tkinter as tk
from tkinter import ttk

def calcular_resultados():
    try:
        # Calcular resultado do campo específico (1 a 20)
        valor = float(entry_input.get())
        if 1 <= valor <= 20:
            resultado_intermediario = 100 * valor / 20
            resultado_final = resultado_intermediario * 0.25
            label_resultado.config(text=f"Resultado: {resultado_final:.2f}")
        else:
            label_resultado.config(text="Digite um valor entre 1 e 20")
            resultado_final = 0  # Define o resultado final como 0 se a entrada for inválida
        
        # Calcular resultados dos 5 pares de NOTA e EIXO com validação
        soma_resultados = 0
        for i in range(5):
            acerto = float(entries_acertos[i].get())
            eixo = float(entries_eixos[i].get())

            # Verificar se os valores estão dentro do intervalo permitido
            if not (1 <= acerto <= 10):
                resultados[i].set("NOTA inválida")
                continue
            if not (1 <= eixo <= 5):
                resultados[i].set("EIXO inválido")
                continue

            resultado = acerto * eixo * 0.55
            resultados[i].set(f"{resultado:.2f}")
            soma_resultados += resultado
        
        # Mostrar a soma dos resultados
        label_soma_resultados.config(text=f"Soma dos Resultados: {soma_resultados:.2f}")
        
        # Calcular e mostrar o resultado final (soma dos resultados dos pares + resultado específico)
        resultado_total = soma_resultados + resultado_final
        label_resultado_total.config(text=f"Resultado Total: {resultado_total:.2f}")

        # Mostrar mensagem elaborada
        label_elaborado.config(text="ELABORADO POR DORVAL")

    except ValueError:
        label_resultado.config(text="Entrada inválida")
        for result in resultados:
            result.set("Entrada inválida")
        label_soma_resultados.config(text="Entrada inválida")
        label_resultado_total.config(text="Entrada inválida")

# Configuração da janela principal
root = tk.Tk()
root.title("Calculadora de Resultados")

# Definindo a fonte (menor)
fonte_padrao = ("Arial", 11)

# Campos de entrada e rótulos para 5 conjuntos de NOTA e EIXO usando Combobox
entries_acertos = []
entries_eixos = []
results_labels = []
resultados = []

for i in range(5):
    tk.Label(root, text=f"NOTA {i+1}:", font=fonte_padrao).grid(row=i*3+1, column=0, padx=10, pady=5)
    entry_acerto = ttk.Combobox(root, values=[str(n) for n in range(1, 11)], font=fonte_padrao, width=5)
    entry_acerto.grid(row=i*3+1, column=1, padx=5, pady=5)
    entries_acertos.append(entry_acerto)
    
    tk.Label(root, text=f"EIXO {i+1}:", font=fonte_padrao).grid(row=i*3+2, column=0, padx=10, pady=5)
    entry_eixo = ttk.Combobox(root, values=[str(n) for n in range(1, 6)], font=fonte_padrao, width=5)
    entry_eixo.grid(row=i*3+2, column=1, padx=5, pady=5)
    entries_eixos.append(entry_eixo)
    
    resultado_var = tk.StringVar()
    label_resultado = tk.Label(root, textvariable=resultado_var, font=fonte_padrao)
    label_resultado.grid(row=i*3+3, column=0, columnspan=2, padx=10, pady=5)
    results_labels.append(label_resultado)
    resultados.append(resultado_var)

# Campo para cálculo específico (1 a 20) usando Combobox
tk.Label(root, text="Digite um número (1 a 20):", font=fonte_padrao).grid(row=16, column=0, padx=10, pady=5)
entry_input = ttk.Combobox(root, values=[str(n) for n in range(1, 21)], font=fonte_padrao, width=5)
entry_input.grid(row=16, column=1, padx=5, pady=5)

# Botão para calcular todos os resultados
button_calcular = tk.Button(root, text="Calcular", font=fonte_padrao, command=calcular_resultados)
button_calcular.grid(row=17, column=0, columnspan=2, padx=5, pady=5, ipadx=5, ipady=2)

# Rótulo para mostrar o resultado do campo específico
label_resultado = tk.Label(root, text="Resultado: ", font=fonte_padrao)
label_resultado.grid(row=18, column=0, columnspan=2, padx=10, pady=5)

# Rótulo para mostrar a soma dos resultados dos pares NOTA e EIXO
label_soma_resultados = tk.Label(root, text="Soma dos Resultados: ", font=fonte_padrao)
label_soma_resultados.grid(row=19, column=0, columnspan=2, padx=10, pady=5)

# Rótulo para mostrar o resultado total
label_resultado_total = tk.Label(root, text="Resultado Total: ", font=fonte_padrao)
label_resultado_total.grid(row=20, column=0, columnspan=2, padx=10, pady=5)

# Rótulo para mostrar mensagem "ELABORADO POR DORVAL"
label_elaborado = tk.Label(root, text="", font=fonte_padrao)
label_elaborado.grid(row=21, column=0, columnspan=2, padx=10, pady=5)

# Ajustar o tamanho da janela para ser menor
root.geometry("414x896")

# Iniciar o loop principal da interface gráfica
root.mainloop()
