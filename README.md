# projeto

import tkinter as tk
from abc import ABC, abstractmethod

# Classe Abstrata Animal
class Animal(ABC):
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

    @abstractmethod
    def mostrar(self):
        pass

    def getNome(self):
        return self.nome

    def getIdade(self):
        return self.idade

    def setNome(self, nome):
        self.nome = nome

    def setIdade(self, idade):
        self.idade = idade

# Classe Cachorro
class Cachorro(Animal):
    def __init__(self, nome, idade, raca, porte):
        super().__init__(nome, idade)
        self.raca = raca
        self.porte = porte

    def mostrar(self):
        return f"Nome: {self.nome}\nIdade: {self.idade}\nRaça: {self.raca}\nPorte: {self.porte}"

    def getRaca(self):
        return self.raca

    def getPorte(self):
        return self.porte

    def setRaca(self, raca):
        self.raca = raca

    def setPorte(self, porte):
        self.porte = porte

# Classe Gato
class Gato(Animal):
    def __init__(self, nome, idade, raca):
        super().__init__(nome, idade)
        self.raca = raca

    def mostrar(self):
        return f"Nome: {self.nome}\nIdade: {self.idade}\nRaça: {self.raca}"

    def getRaca(self):
        return self.raca

    def setRaca(self, raca):
        self.raca = raca

# Lista de animais
animais = []

# Função para cadastrar animal
def cadastrar_animal():
    nome = entry_nome.get()
    idade = int(entry_idade.get())
    raca = entry_raca.get()
    porte = entry_porte.get()

    if var_tipo.get() == "Cachorro":
        animal = Cachorro(nome, idade, raca, porte)
    else:
        animal = Gato(nome, idade, raca)

    animais.append(animal)
    limpar_campos()

# Função para listar animais
def listar_animais():
    texto_lista.delete(1.0, tk.END)
    for animal in animais:
        texto_lista.insert(tk.END, animal.mostrar() + "\n\n")

# Função para limpar campos
def limpar_campos():
    entry_nome.delete(0, tk.END)
    entry_idade.delete(0, tk.END)
    entry_raca.delete(0, tk.END)
    entry_porte.delete(0, tk.END)

# Criar janela principal
janela = tk.Tk()
janela.title("Cadastro de Animais")

# Criar abas
aba_cadastro = tk.Frame(janela)
aba_lista = tk.Frame(janela)

aba_cadastro.pack(fill="both", expand=True)
aba_lista.pack(fill="both", expand=True)

# Criar widgets para cadastro
label_nome = tk.Label(aba_cadastro, text="Nome:")
label_nome.pack()
entry_nome = tk.Entry(aba_cadastro)
entry_nome.pack()

label_idade = tk.Label(aba_cadastro, text="Idade:")
label_idade.pack()
entry_idade = tk.Entry(aba_cadastro)
entry_idade.pack()

label_raca = tk.Label(aba_cadastro, text="Raça:")
label_raca.pack()
entry_raca = tk.Entry(aba_cadastro)
entry_raca.pack()

label_porte = tk.Label(aba_cadastro, text="Porte:")
label_porte.pack()
entry_porte = tk.Entry(aba_cadastro)
entry_porte.pack()

var_tipo = tk.StringVar()
var_tipo.set("Cachorro")
opcoes_tipo = ["Cachorro", "Gato"]
menu_tipo = tk.OptionMenu(aba_cadastro, var_tipo, *opcoes_tipo)
menu_tipo.pack()

botao_cadastrar = tk.Button(aba_cadastro, text="Cadastrar", command=cadastrar_animal)
botao_cadastrar.pack()

# Criar widgets para lista
texto_lista = tk.Text(aba_lista)
texto_lista.pack(fill="both", expand=True)

botao_listar = tk.Button(aba_lista, text="Listar Animais", command=listar_animais)
botao_listar.pack()

janela.mainloop()
