# model_converter
Questo notebook guida il processo di conversione del modello di Object Detection utilizzato nell'app InfoTarghe, da TensorFlow in TensorFlow Lite con l'aggiunta di metadati rispettando i vincoli di compatibilità con l'API di Object Detection per Android

# 📌 Configurazione dell'Ambiente Virtuale (smconverter)

Descrivo **i passaggi eseguiti** per creare e configurare l'ambiente virtuale **smconverter** necessario per eseguire il notebook di conversione.

---

## 1️⃣ Installazione di Chocolatey
Per installare **Chocolatey**, ho eseguito il seguente comando in **Prompt dei Comandi con privilegi di amministratore**:

```powershell
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

Dopo l'installazione, ho verificato che fosse installato correttamente con:
```powershell
choco --version
```

---

## 2️⃣ Installazione di Python 3.9
Sul mio sistema era già presente **Python 3.13.1**, quindi ho dovuto installare la versione **3.9.13** forzando il downgrade:

```powershell
choco install python --version=3.9.13 -y --allow-downgrade
```

Dopo l'installazione, ho verificato la versione installata:
```powershell
python --version
```
✅ **Output atteso:** `Python 3.9.13`

---

## 3️⃣ Creazione dell'Ambiente Virtuale
Ho creato l'ambiente virtuale **smconverter** specificando Python 3.9:

```powershell
C:\Python39\python.exe -m venv smconverter
```

Per attivarlo:
```powershell
smconverter\Scripts\activate
```

Verifica dell'ambiente virtuale:
```powershell
python --version
```
✅ **Output atteso all'interno del venv:** `Python 3.9.13`

---

## 4️⃣ Installazione di pip e aggiornamenti
Ho riscontrato un errore di accesso negato durante l'aggiornamento di `pip`, quindi ho usato il seguente comando per reinstallarlo e aggiornarlo:

```powershell
python -m ensurepip --default-pip
python -m pip install --upgrade pip setuptools wheel
```

Verifica della versione di `pip`:
```powershell
pip --version
```
✅ **Output:** `pip 25.0 from S:\PROGETTO\smconverter\lib\site-packages\pip (python 3.9)`

---

## 5️⃣ Installazione delle dipendenze
Successivamente, ho installato le librerie necessarie:

```powershell
pip install notebook
pip install tensorflow 
pip install tflite-support
pip install protobuf

```
Verifica delle versioni installate:
```powershell
pip show tensorflow
pip show protobuf
pip show tflite-support
```

✅ **Output:**
```
tensorflow 2.18.0
protobuf 5.29.3
tflite-support 0.4.3

```

ℹ **Nota su `tflite-support`**  
La libreria **tflite-support** è necessaria per poter eseguire lo script predefinito che aggiunge i **metadati al modello**, rispettando i vincoli di compatibilità imposti dall’API di Object Detection di TensorFlow Lite.  
L'ultima versione attualmente disponibile è **0.4.3**.  

⚠ **Problema di compatibilità:**  
`tflite-support` **non è compatibile con Python 3.10 e versioni successive**, quindi è stato necessario utilizzare Python **3.9.13**, che è l'ultima versione completamente supportata.

---

## 6️⃣ Avvio di Jupyter Notebook
Ora che l'ambiente è pronto, avvio Jupyter eseguendo:

```powershell
jupyter notebook
```

Si aprirà il browser e potrò selezionare e avviare il notebook di conversione:
model_converter.ipynb



