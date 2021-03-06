#!/usr/bin/env/python
#coding: cp1250 

import wx

def Zamknij(event):
	Dialog = wx.MessageDialog(Okno, u'Czy na pewno?', u'Koniec pracy',
				  style=wx.OK | wx.CANCEL)
	odpowiedz = Dialog.ShowModal()
	Dialog.Destroy()
	if odpowiedz == wx.ID_OK:
		Okno.Close()

def Otworz_Fasta(event):
	Dialog=wx.FileDialog(Okno, message='Wybierz plik FASTA', defaultFile='',
			     wildcard='*.FASTA', style=wx.OPEN | wx.MULTIPLE | wx.CHANGE_DIR)
	if Dialog.ShowModal() != wx.ID_OK:
		return
	plik_sciezka = Dialog.GetPaths()
	plik_tekst = open(plik_sciezka[0], 'r')
	odczyt = plik_tekst.read().splitlines()
	plik_tekst.close()
	
	sekwencje[ : ] = [] 
	nazwy[ : ] =[]
	
	nazwa=''
	for linia in odczyt:
		if linia[0] == '>':
			if nazwa != '':
				sekwencje.append([gi, gb, nazwa, sekw])
				nazwy.append(nazwa)
			podzielona_linia = linia.split('|')
			gi = podzielona_linia[1]
			gb = podzielona_linia[3]
			nazwa = podzielona_linia[4]
			sekw = ''
		else:
			sekw += linia
	sekwencje.append([gi, gb, nazwa, sekw])
	nazwy.append(nazwa)

	Lista_Nazw.SetItems(nazwy)
	Lista_Nazw.Show()
	Lista_Obliczen.Show()
	Lista_Obliczen.SetItems([])
	Dialog.Destroy()
	
def Otworz_GenBank(event):
        Dialog=wx.FileDialog(Okno, message='Wybierz plik GENBANK', defaultFile='',
                                 wildcard='*.seq', style=wx.OPEN | wx.MULTIPLE | wx.CHANGE_DIR)
        if Dialog.ShowModal() != wx.ID_OK:
                return
        plik_sciezka = Dialog.GetPaths()
        plik_tekst = open(plik_sciezka[0], 'r')
        odczyt = plik_tekst.read().splitlines()
        plik_tekst.close()
        
        sekwencje[:] = [] # Zresetowanie zmiennych przy każdym wczytaniu pliku 
        nazwy[:] = []
        nazwa = ''
        for linia in odczyt:
          podzielona_linia = linia.split()
          if podzielona_linia == []:
               podzielona_linia.append('pusta')
          if podzielona_linia[0] == 'DEFINITION':
               nazwa = podzielona_linia[1:]
               nazwy.append(nazwa)
          if podzielona_linia[0] == 'VERSION':
               gi = podzielona_linia[2]
               gi.append(gi)
          if podzielona_linia[0] == 'ORIGIN':
               org = podzielona_linia
          else:
               sekw += org [1][n]
          sekwencje.append([defi,gi,org])
          nazwy.append(nazwa)
	
    
                   
        Lista_Nazw.SetItems(nazwy)
        Lista_Nazw.Show()
        Lista_Obliczen.Show()
        Lista_Obliczen.SetItems([])
        Dialog.Destroy()

def Oblicz_Score(event):
        n = Lista_Nazw.GetSelection()
        n = sekwencje[0][3]
        n2=sekwencje[1][3]
        ilosci = []
        for z in range (len(n2)):
                if n2[z]!=n[z]:
                        n2=n2[:z]+"-"+n2[z:]
                if len(n2) == len(n):
                        break
        for i in range(len(n)):
                if n[i] == n2[i] or n[i] == n2[i+1]:
                        ilosci.append('[ '+str(i)+' ('+n[i]+','+str(n.count(n[i]))+') ]')
        Lista_Obliczen.SetItems(ilosci)

def Oblicz_Score1(event):
        n = Lista_Nazw.GetSelection()
        n = sekwencje[-1][3]
        n2=sekwencje[-2][3]
        ilosci = []
        for z in range (len(n2)):
                if n2[z]!=n[z]:
                        n2=n2[:z]+"-"+n2[z:]
                if len(n2) == len(n):
                        break
        for i in range(len(n)):
                if n[i] == n2[i] or n[i] == n2[i+1]:
                        ilosci.append('[ '+str(i)+' ('+n[i]+','+str(n.count(n[i]))+') ]')
        Lista_Obliczen.SetItems(ilosci)
sekwencje = []
nazwy = []
gi=[]

 #Rozpoczęcie nowej aplikacji
Prog = wx.PySimpleApp()

 #Utworzenie okna i list
Okno = wx.Frame(parent=None, title=u'Menu programu', size=(900, 700))
Panel = wx.Panel(parent=Okno)

Lista_Nazw = wx.ListBox(parent=Panel, pos=(30, 30), size=(500, 500))
Lista_Nazw.Hide()

Lista_Obliczen = wx.ListBox(parent=Panel, pos=(560, 30), size=(300, 500))
Lista_Obliczen.Hide()



# Utworzenie paska menu
Pasek_Menu = wx.MenuBar()

Menu_Dane = wx.Menu()
Menu_Dane_Fasta = Menu_Dane.Append(wx.ID_ANY, u'Czytaj Fasta')
Okno.Bind(wx.EVT_MENU, Otworz_Fasta, Menu_Dane_Fasta)
Menu_Dane_GenBank = Menu_Dane.Append(wx.ID_ANY, u'Czytaj GenBank')
Okno.Bind(wx.EVT_MENU, Otworz_GenBank, Menu_Dane_GenBank)
Pasek_Menu.Append(Menu_Dane, u'Dane')

Menu_Obliczenia = wx.Menu()
Menu_Obliczenia_Score=Menu_Obliczenia.Append(wx.ID_ANY, u'Oblicz koincydencje od lewej strony')
Okno.Bind(wx.EVT_MENU, Oblicz_Score, Menu_Obliczenia_Score)
Menu_Obliczenia_Score=Menu_Obliczenia.Append(wx.ID_ANY, u'Oblicz koincydencje od prawej strony')
Okno.Bind(wx.EVT_MENU, Oblicz_Score1, Menu_Obliczenia_Score)
Pasek_Menu.Append(Menu_Obliczenia, u'Obliczenia')

Menu_Wyjscie = wx.Menu()
Menu_Wyjscie_Koniec = Menu_Wyjscie.Append(wx.ID_EXIT, u'Koniec')
Okno.Bind(wx.EVT_MENU, Zamknij, Menu_Wyjscie_Koniec)
Pasek_Menu.Append(Menu_Wyjscie, u'Wyjscie')

Okno.SetMenuBar(Pasek_Menu)


Okno.Show()
Prog.MainLoop()
