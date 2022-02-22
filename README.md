$ pip3 install SpeechRecognition
$ pip3 install pyaudio

import speech_recognition as sr


def reconhece():
	rec = sr.Recognizer()

	with sr.Microphone() as s:
		rec.adjust_for_ambient_noise(s)

		while True:
			try:
				audio = rec.listen(s)
				entrada = rec.recognize_google(audio, language="pt")
				return "Você disse: {}".format(entrada)
			except sr.UnknownValueError:
				return "Não entendi nada"
			

print("Ouvindo...\n-----------------\n")
while True:
	fala = reconhece()
	print(fala)
  
  import speech_recognition as sr
import pyttsx3
from random import choice


lista_erros = [
		"Não entendi nada",
		"Desculpe, não entendi",
		"Repita novamente por favor"
]


reproducao = pyttsx3.init()


def sai_som(reposta):
	reproducao.say(reposta)
	reproducao.runAndWait()


def reconhece(resposta_erro_aleatoria):
	rec = sr.Recognizer()

	with sr.Microphone() as s:
		rec.adjust_for_ambient_noise(s)

		while True:
			try:
				audio = rec.listen(s)
				entrada = rec.recognize_google(audio, language="pt")
				return "{}".format(entrada)
			except sr.UnknownValueError:
				return resposta_erro_aleatoria
			

print("Ouvindo...\n-----------------\n")
while True:
	resposta_erro_aleatoria = choice(lista_erros)
	fala = reconhece(resposta_erro_aleatoria)
	print("Você disse: {}".format(fala))
	sai_som(fala)
  
  mport speech_recognition as sr
import pyttsx3
from config import *
from random import choice

reproducao = pyttsx3.init()

def sai_som(reposta):
	reproducao.say(reposta)
	reproducao.runAndWait()


print("Ouvindo...\n-----------------\n")
while True:
	resposta_erro_aleatoria = choice(lista_erros)
	rec = sr.Recognizer()

	with sr.Microphone() as s:
		rec.adjust_for_ambient_noise(s)

		while True:
			try:
				audio = rec.listen(s)
				entrada = rec.recognize_google(audio, language="pt")
				print("Você disse: {}".format(entrada))

				reposta = conversas[entrada]

				print("Assistente: {}".format(reposta))
				sai_som("{}".format(reposta))

			except sr.UnknownValueError:
				sai_som(resposta_erro_aleatoria)
        
        lista_erros = [
		"Não entendi nada",
		"Desculpe, não entendi",
		"Repita novamente por favor"
]

conversas = {
	"Olá": "oi, tudo bem?",
	"sim e você": "Estou bem obrigada por perguntar",
}

comandos = {
	"desligar": "desligando",
	"reiniciar": "reiniciando"
}
import speech_recognition as sr
import pyttsx3
from config import *
from random import choice

reproducao = pyttsx3.init()

def sai_som(reposta):
	reproducao.say(reposta)
	reproducao.runAndWait()

def assistente():
	print("Oi, qual  é o seu nome completo")
	sai_som("Oi, qual é o seu nome completo")
	while True:
		resposta_erro_aleatoria = choice(lista_erros)
		rec = sr.Recognizer()

		with sr.Microphone() as s:
			rec.adjust_for_ambient_noise(s)

			while True:
				try:
					audio = rec.listen(s)
					user_name = rec.recognize_google(audio, language="pt")
					user_name = verifica_nome(user_name)
					name_list()
					apresentacao = "{}".format(verifica_nome_exist(user_name))
					print(apresentacao)
					sai_som(apresentacao)
		
					brute_user_name = user_name
					user_name = user_name.split(" ")
					user_name = user_name[0]
					break
				except sr.UnknownValueError:
					sai_som(resposta_erro_aleatoria)
			break


	print("="* len(apresentacao))
	print("Ouvindo...")

	while True:
		resposta_erro_aleatoria = choice(lista_erros)
		rec = sr.Recognizer()

		with sr.Microphone() as s:
			rec.adjust_for_ambient_noise(s)

			while True:
				try:
					audio = rec.listen(s)
					entrada = rec.recognize_google(audio, language="pt")
					print("{}: {}".format(user_name, entrada))

					reposta = conversas[entrada]

					print("Assistente: {}".format(reposta))
					sai_som("{}".format(reposta))

				except sr.UnknownValueError:
					sai_som(resposta_erro_aleatoria)


if __name__ == '__main__':
	intro()
	sai_som("Iniciando")
	assistente()
  
  version = "1.5.0"


def intro():
	msg = "Assistente - version {} / by: Fulano beltrano ciclano".format(version)
	print("-" * len(msg) +  "\n{}\n".format(msg)  +   "-" * len(msg))


lista_erros = [
		"Não entendi nada",
		"Desculpe, não entendi",
		"Repita novamente por favor"
]

conversas = {
	"Olá": "oi, tudo bem?",
	"sim e você": "Estou bem obrigada por perguntar",
}

comandos = {
	"desligar": "desligando",
	"reiniciar": "reiniciando"
}


def verifica_nome(user_name):
	if user_name.startswith("Meu nome é"):
		user_name = user_name.replace("Meu nome é", "")
	if user_name.startswith("Eu me chamo"):
		user_name = user_name.replace("Eu me chamo", "")
	if user_name.startswith("Eu sou o"):
		user_name = user_name.replace("Eu sou o", "")
	if user_name.startswith("Eu sou a"):
		user_name = user_name.replace("Eu sou a", "")

	return user_name 


def  verifica_nome_exist(nome):
	dados = open("dados/nomes.txt", "r")
	nome_list = dados.readlines()

	if not nome_list:
		vazio = open("dados/nomes.txt", "r")
		conteudo = vazio.readlines()
		conteudo.append("{}".format(nome))
		vazio = open("dados/nomes.txt", "w")
		vazio.writelines(conteudo)
		vazio.close()

		return "Olá {}, prazer em te conhecer!".format(nome)

	for linha in nome_list:
		if linha == nome:
			return "Olá {}, acho que já nos conhecemos".format(nome)

	vazio = open("dados/nomes.txt", "r")
	conteudo = vazio.readlines()
	conteudo.append("\n{}".format(nome))
	vazio = open("dados/nomes.txt", "w")
	vazio.writelines(conteudo)
	vazio.close()

	return "Oi {} é a primeira vez que nos falamos".format(nome)


def name_list():
	try:
		nomes = open("dados/nomes.txt", "r")
		nomes.close()

	except FileNotFoundError:
		nomes = open("dados/nomes.txt", "w")
		nomes.close()


def calcula(entrada):
	if "mais" in entrada or "+" in entrada:
		# É soma
		entradas_recebidas = entrada.split(" ")
		resultado = int(entradas_recebidas[1]) + int(entradas_recebidas[3])

	elif "menos" in entrada or "-" in entrada:
		# É subtração

		entradas_recebidas = entrada.split(" ")
		resultado = int(entradas_recebidas[1]) - int(entradas_recebidas[3])

	elif "vezes" in entrada or "x" in entrada:
		# É vezes

		entradas_recebidas = entrada.split(" ")
		resultado = round(float(entradas_recebidas[1]) * float(entradas_recebidas[3]), 2)

	elif "dividido" in entrada or "/" in entrada:
		# É divisão

		entradas_recebidas = entrada.split(" ")
		resultado = round(float(entradas_recebidas[1]) / float(entradas_recebidas[4]), 2)

	else:

		resultado = "Operação não encontrada"


	return resultado
  
  import speech_recognition as sr
import pyttsx3
from config import *
from random import choice

reproducao = pyttsx3.init()

def sai_som(reposta):
	reproducao.say(reposta)
	reproducao.runAndWait()

def assistente():
	print("Oi, qual  é o seu nome completo")
	sai_som("Oi, qual é o seu nome completo")
	while True:
		resposta_erro_aleatoria = choice(lista_erros)
		#rec = sr.Recognizer()

		#with sr.Microphone() as s:
			#rec.adjust_for_ambient_noise(s)

		while True:
			try:
				#audio = rec.listen(s)
				user_name = input("")
				user_name = verifica_nome(user_name)
				name_list()
				apresentacao = "{}".format(verifica_nome_exist(user_name))
				print(apresentacao)
				sai_som(apresentacao)
		
				brute_user_name = user_name
				user_name = user_name.split(" ")
				user_name = user_name[0]
				break
			except sr.UnknownValueError:
				sai_som(resposta_erro_aleatoria)
		break


	print("="* len(apresentacao))
	print("Ouvindo...")

	while True:
		resposta_erro_aleatoria = choice(lista_erros)
		#rec = sr.Recognizer()

		#with sr.Microphone() as s:
			#rec.adjust_for_ambient_noise(s)

		while True:
			try:
				# audio = rec.listen(s)
				entrada = input("")
				print("{}: {}".format(user_name, entrada))

				# Operações matemáticas
				if "quanto é" in entrada:

					entrada = entrada.replace("quanto é", "")
					reposta = calcula(entrada)
				else:
					reposta = conversas[entrada]

				print("Assistente: {}".forma
        
        
        mport requests as rq


version = "1.5.0"
cidade = 'joinville'

def intro():
	msg = "Assistente - version {} / by: Fulano beltrano ciclano".format(version)
	print("-" * len(msg) +  "\n{}\n".format(msg)  +   "-" * len(msg))


lista_erros = [
		"Não entendi nada",
		"Desculpe, não entendi",
		"Repita novamente por favor"
]

conversas = {
	"Olá": "oi, tudo bem?",
	"sim e você": "Estou bem obrigada por perguntar",
}

comandos = {
	"desligar": "desligando",
	"reiniciar": "reiniciando"
}


def verifica_nome(user_name):
	if user_name.startswith("Meu nome é"):
		user_name = user_name.replace("Meu nome é", "")
	if user_name.startswith("Eu me chamo"):
		user_name = user_name.replace("Eu me chamo", "")
	if user_name.startswith("Eu sou o"):
		user_name = user_name.replace("Eu sou o", "")
	if user_name.startswith("Eu sou a"):
		user_name = user_name.replace("Eu sou a", "")

	return user_name 


def  verifica_nome_exist(nome):
	dados = open("dados/nomes.txt", "r")
	nome_list = dados.readlines()

	if not nome_list:
		vazio = open("dados/nomes.txt", "r")
		conteudo = vazio.readlines()
		conteudo.append("{}".format(nome))
		vazio = open("dados/nomes.txt", "w")
		vazio.writelines(conteudo)
		vazio.close()

		return "Olá {}, prazer em te conhecer!".format(nome)

	for linha in nome_list:
		if linha == nome:
			return "Olá {}, acho que já nos conhecemos".format(nome)

	vazio = open("dados/nomes.txt", "r")
	conteudo = vazio.readlines()
	conteudo.append("\n{}".format(nome))
	vazio = open("dados/nomes.txt", "w")
	vazio.writelines(conteudo)
	vazio.close()

	return "Oi {} é a primeira vez que nos falamos".format(nome)


def name_list():
	try:
		nomes = open("dados/nomes
    
    
    
        





# Gijoe
