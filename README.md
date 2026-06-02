# Programa-o-de-computadores-
Projeto em python:
**Resumo do Projeto**

Este projeto consiste em um sistema de gerenciamento escolar desenvolvido em Python, utilizando conceitos de funções, listas, dicionários, estruturas de repetição e validação de dados.

O sistema possui uma lista fixa com 20 alunos e 5 disciplinas (Português, Matemática, Biologia, Química e Física). Para cada aluno, o usuário informa duas notas e a quantidade de faltas em cada disciplina. O programa calcula automaticamente a média das notas e determina a situação do aluno em cada matéria, considerando os critérios de aprovação por nota (média igual ou superior a 6) e reprovação por faltas (51 faltas ou mais).

Além disso, o sistema gera um relatório completo contendo o desempenho de cada aluno, exibindo as médias, faltas e situação em cada disciplina, bem como a média geral do aluno. Ao final, apresenta um resumo com a quantidade total de alunos aprovados e reprovados.

O projeto tem como objetivo aplicar os principais conceitos de Estrutura de Dados e Programação em Python, demonstrando o uso de funções, validação de entradas, listas, dicionários e geração de relatórios.

# =====================================
# FUNÇÕES DE VALIDAÇÃO
# =====================================

def obter_nota_valida(mensagem):
    while True:
        try:
            nota = float(input(mensagem))

            if 0 <= nota <= 10:
                return nota

            print("Nota inválida. Digite um valor entre 0 e 10.")

        except ValueError:
            print("Entrada inválida. Digite um número válido.")


def obter_faltas_validas(mensagem):
    while True:
        try:
            faltas = int(input(mensagem))

            if faltas >= 0:
                return faltas

            print("A quantidade de faltas não pode ser negativa.")

        except ValueError:
            print("Entrada inválida. Digite um número inteiro.")


# =====================================
# CÁLCULO DE MÉDIA
# =====================================

def calcular_media(nota1, nota2):
    return (nota1 + nota2) / 2


# =====================================
# SITUAÇÃO DO ALUNO
# =====================================

def verificar_situacao(media, faltas):

    if faltas >= 51:
        return "Reprovado por faltas"

    elif media >= 6:
        return "Aprovado"

    else:
        return "Reprovado por nota"


# =====================================
# CADASTRO DE ALUNOS
# =====================================

def cadastrar_alunos():

    disciplinas_escola = [
        "Português",
        "Matemática",
        "Biologia",
        "Química",
        "Física"
    ]

    alunos_fixos = [
        "Ana Beatriz Silva",
        "Bruno Costa Santos",
        "Carlos Henrique Souza",
        "Daniel Oliveira Lima",
        "Eduarda Martins Rocha",
        "Felipe Almeida Costa",
        "Gabriela Ferreira Silva",
        "Gustavo Pereira Santos",
        "Helena Rodrigues Alves",
        "Igor Carvalho Rocha",
        "Julia Mendes Costa",
        "Larissa Gomes Silva",
        "Lucas Barbosa Pereira",
        "Mariana Alves Souza",
        "Matheus Ferreira Lima",
        "Nicolas Rocha Santos",
        "Paula Cristina Oliveira",
        "Rafael Gomes Costa",
        "Sofia Martins Silva",
        "Thiago Henrique Alves"
    ]

    lista_alunos = []

    for nome in alunos_fixos:

        print(f"\n================================")
        print(f"Cadastro de notas - {nome}")
        print("================================")

        disciplinas_aluno = []

        for materia in disciplinas_escola:

            print(f"\nDisciplina: {materia}")

            nota1 = obter_nota_valida(
                "Digite a nota do primeiro semestre: "
            )

            nota2 = obter_nota_valida(
                "Digite a nota do segundo semestre: "
            )

            faltas = obter_faltas_validas(
                "Digite a quantidade de faltas: "
            )

            media = calcular_media(nota1, nota2)

            situacao = verificar_situacao(
                media,
                faltas
            )

            disciplina = {
                "materia": materia,
                "media": media,
                "faltas": faltas,
                "situacao": situacao
            }

            disciplinas_aluno.append(disciplina)

        aluno = {
            "nome": nome,
            "disciplinas": disciplinas_aluno
        }

        lista_alunos.append(aluno)

    return lista_alunos


# =====================================
# RELATÓRIO FINAL
# =====================================

def gerar_relatorio_final(alunos):

    aprovados = 0
    reprovados = 0

    print("\n========== RELATÓRIO FINAL ==========")

    for aluno in alunos:

        print(f"\nAluno: {aluno['nome']}")

        soma_medias = 0

        for disciplina in aluno["disciplinas"]:

            soma_medias += disciplina["media"]

            print(f"\nDisciplina: {disciplina['materia']}")
            print(f"Média: {disciplina['media']:.2f}")
            print(f"Faltas: {disciplina['faltas']}")
            print(f"Situação: {disciplina['situacao']}")

        media_geral = soma_medias / len(aluno["disciplinas"])

        print(f"\nMédia Geral: {media_geral:.2f}")

        aluno_aprovado = True

        for disciplina in aluno["disciplinas"]:

            if disciplina["situacao"] != "Aprovado":
                aluno_aprovado = False
                break

        if aluno_aprovado:
            aprovados += 1
        else:
            reprovados += 1

    print("\n================================")
    print("RESUMO GERAL")
    print("================================")
    print(f"Total de aprovados: {aprovados}")
    print(f"Total de reprovados: {reprovados}")


# =====================================
# MENU PRINCIPAL
# =====================================

alunos_cadastrados = []

while True:

    print("\n========== MENU ==========")
    print("1 - Cadastrar notas")
    print("2 - Exibir relatório")
    print("3 - Sair")

    opcao = input("Escolha uma opção: ")

    if opcao == "1":

        alunos_cadastrados = cadastrar_alunos()

    elif opcao == "2":

        if len(alunos_cadastrados) == 0:
            print("Nenhum aluno cadastrado.")
        else:
            gerar_relatorio_final(alunos_cadastrados)

    elif opcao == "3":

        print("Programa encerrado.")
        break

    else:

        print("Opção inválida.")
