 DockerParaGPU
muestro los comandos utiles para crear un docker de tensorflow

Primero instalar docker

Despues crear el archivo docker debe llamarse Dockerfile:

interior del archivo 
*********************************************************************
#Empezar con una imagen base de CUDA con TensorFlow

FROM tensorflow/tensorflow:latest-gpu

#Configurar el directorio de trabajo
WORKDIR /app

#Copiar y crear el entorno Conda
COPY requirements.txt /app/requirements.txt
#RUN pip install -r /app/requirements.txt 

#Exponer el puerto 8888
EXPOSE 8888

#Copiar los archivos de la aplicación
COPY . /app

#Comando para iniciar Jupyter Notebook
CMD ["jupyter", "notebook", "--notebook-dir=/app", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]

*********************************************************************
en la misma carpeta agregar el archivo requiremetents.txt con las versiones de pip que queremos instalar

interior del archivo 
*********************************************************************
h5py
scikit-learn==1.3.0
pandas==2.0.3
matplotlib==3.7.2
scipy==1.10.1
ray==2.6.1
numpy==1.23.5
psutil==5.9.0
jupyter
pandarallel==1.6.4
astropy==5.1
plotly==5.9.0
seaborn==0.12.2
imbalanced-learn==0.11.0
wget
*********************************************************************
despues construir el docker

sudo docker build -t nombre .

el nombre que le asigne es deep

abrir la imagen utilizando todas las gpu, asignando el puerto para el jupyter, montando el home, llamando la imagen que creamos y asignando bash para que sea interactivo 

sudo docker run -it --gpus all -p 8888:8888 -v /home/nicolas:/home/nicolas deep /bin/bash

moverse por la terminal a la carpeta donde queremos abrir el jupyter notebook y utilizar 

jupyter notebook --allow-root --ip=0.0.0.0 --no-browser

listo!!
