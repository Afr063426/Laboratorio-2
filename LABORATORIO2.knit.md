---
output:
  pdf_document:
    toc: true
    toc_depth: 2
    includes:
      in_header: preambulo.tex
      before_body: titulo.tex
     
documentclass: memoir
classoption: oneside

---









\chapter{Resumen Ejecutivo 1}
Aquí debe dar resultados generales de lo que obtuvo del análisis.

\chapter{Introducción 1}

\chapter{Objetivos 1}

\section{Objetivo general}

Analizar la curva de rendimiento de los bonos del tesoro de Estados Unidos de Norte América por medio del modelo de Nelson y Siegel en el periodo de años comprendido entre el 1° de enero del 2010 y el  20 de mayo del 2021.

\section{Objetivos específicos}
\begin{enumerate} 

\item Explicar el modelo de Nelson y Siegel.

\item Describir las características de la base de datos de los bonos del tesoro de Estados Unidos de Norte América.

\item Implementar el modelo de Nelson y Siegel en lenguaje de programación R, para la base de datos de los bonos del tesoro de Estados Unidos de Norte América.

\item Evaluar los resultados obtenidos apartir del modelo de Nelson y Siegel.

\end{enumerate}





\chapter{Marco teórico 3}
\par La curva de rendimiento es una herramienta útil a la hora de quererse invertir o negociar un instrumento financiero y al momento de aplicar políticas monetarias.

\par \textbf{rendimientos spot definir}
\par Se procede a explicar qué es la curva de rendimiento, según Boudreault y Reanud (2019) la curva de rendimiento también llamada curva de rendimientos spot. Esta curva muestra la relación que hay entre las tasa de rendimiento spot y el tiempo de maduración. Así esta curva muestra los rendimientos que se obtienen de mantener una cierta cantidad de dinero durante un tiempo determinado. Se puede determinar el rendimiento mediante
\[
y=\left(\frac{F}{B_0}\right)^{\frac{1}{T}}-1
\]
Donde 
\begin{table}[H]
\begin{tabular}{c|c}
$y$ & Tasa de rendimiento\\
$T$ & Tiempo para la maduración\\
$B_0$ & Costo de la inversión o precio del bono\\
$F$ & Monto a recibir al final del periodo
\end{tabular}
\end{table}
\par Sin embargo a pesar de que esta herramienta es ampliamente utilizada, tiene una limitante intertemporal. Como lo expone Camilo (2008) esta se construye a través de una serie de tasas (precios) de instrumentos financieros discontinuos en el tiempo. Esto implica que entonces lo se ubica a partir de las tasas de rendimiemto es una serie de puntos que no reflejan de forma continua las tasas de rendimiento en el mercado financiero de acuerdo a su tiempo de maduración.
\par Sin embargo hay agentes los cuales no están dispuestos a invertir o prestar los montos al tiempo establecido por agentes como los gobiernos nacionales u otras empresas. Es por esta razón que sería de utilidad encontrar una curva suave la cual sea capaz de proyectar las tasas de rendimiento en distintos momentos del tiempo, pero basado en lo que anteriormente han establecido agentes como los gobiernos nacionales.
\par Para lograr obtener una curva suave la cual se aproxime a las tasas de rendimiento de agentes como los gobiernos, se emplean distintos métodos entre ellos los métodos paramétricos que están basados en la construcción de curvas a partir de modelos paramétricos. (Choudhry, 2010)
\par Entre los modelos paramétricos se encuentra el de Nelson-Siegel. El cual según Matteson (2015) describe las tasas forward con la siguiente curva
\[
r(t,\theta)=\theta_0+(\theta_1+\theta_2t)\exp(-\theta_3 t)
\]
A partir de esta se puede obtener que la curva de rendimiento continua se puede obtener haciendo
\[
\begin{split}
y(t,\theta)&=t^{-1}\int_{0}^{t}r(x,\theta)dx\\
&=\theta_0+\left(\theta_1+\frac{\theta_2}{\theta_3}\right)\frac{1-\exp(-\theta_3 t)}{\theta_3 t}-\frac{\theta_2}{\theta_3}\exp(-\theta t)
\end{split}
\]
Tal y como lo citan Hladíková y Radová (2012) este modelo tiene una interpretación económica interesante para los parámetros. Tomando la curva que describe las tasas forward 
Primero
\[
\lim_{t\to\infty}r(t,\theta)=\theta_{0}\qquad \lim_{t\to 0}r(t,\theta)=\theta_0+\theta_1
\]
\begin{itemize}
\item Entonces $\beta_0>0$ representa la asintota horizontal de la curva 
\end{itemize}





\chapter{Descripción de los datos 5}

\par Profesora, estuvimos investigado bases de datos donde nos dieran como insumo el precio de los bonos, nos encontramos con varios inconvenientes de las misma:
\par 1.	El registro de datos es muy corto, aproximadamente 1 mes como mucho, más que todo datos eran de un día especifico y no guardan registro de los anteriores.
\par 2.	En Bonos cero cupones, para calcular las tasas, el plazo de maduración máximo fue a 10 años, posterior a 10 años tienen cupón y no se puede hacer bootstrapping.
\par 3.	No se tiene presente la tasa de descuento para estos bonos de más de 10 años, por lo que no se puede traer a valor presente, para calcular su respectiva tasa de pendiente 
\par 4.	Estos inconvenientes se mantenían en todas las bases de datos que hemos encontrado, las cuales han sido muy pocas por el siguiente punto.
\par 5.	En sus mayorías las bases de datos con una cantidad aceptable de observaciones se encuentran las tasas de rendimiento (spot) 
\par Tal vez nos podría dar alguna indicación con respecto a estas bases de datos o sugerir una en específico, para así poder avanzar en el desarrollo del proyecto o en su defecto trabajarlo solo con las bases de datos que contienen a las tasas de rendimientos, como la que se está trabajando en este momento.
\par Por lo anterior le presentamos dos ideas para desarrollar el trabajo, la primera partiendo de los precios de los bonos con una base de datos que a nuestro parecer no es la mejor, pues no cuenta con amplitud de observaciones ni rendimientos a largo plazo y la segunda con una base de datos que cuenta con las tasas de rendimiento únicamente, pero con grandes cantidades de observaciones y amplitud de fechas de maduración.


\section{Opción 1}

\section{Opción 2}
Grafico de todos los datos:


```r
Datosgra10Y<-gather(datos10Y, "Fecha de maduración", Obtenido, names(datos10Y[2]):names(datos10Y[length(datos10Y)]))

ggplot( data =Datosgra10Y, mapping = aes(x = Date, y = Obtenido, group=`Fecha de maduración`, color=`Fecha de maduración`)) + 
    geom_line()+
    scale_color_discrete(labels=c("1 mes", "6 meses", "1 año", "2 años", "3 años","5 años","7 años", "10 años","20 años","30 años"))+
      labs(
      y = "Tasa de rendimiento en %",
      x = "Tiempo",
      title = "Comportamiento de las tasas spot"
      ) +
    theme(legend.position="bottom")+
    theme(plot.title = element_text(hjust = .5))# colocamos el titulo en el centro
```

![](LABORATORIO2_files/figure-latex/unnamed-chunk-3-1.pdf)<!-- --> 


Promedio y Desviación de los 3 


```r
# ggplot( data= promedios10Y , mapping = aes(x = Maduration, y = Rendimiento)) + 
#     geom_point()+
#     geom_point(data= promedios10Y, mapping = aes(x = Maduration, y =Varianza))+
#   xlab('Fecha de maduración') + 
#   ylab('Tasas spot') +
#   ggtitle('Distribución de las tasa spot') + 
#     theme(legend.position="bottom")+
#     theme(plot.title = element_text(hjust = .5))# colocamos el titulo en el centro
```



```r
# ggplot(Datosgra10Y) +
#   geom_density(aes(x = Obtenido, fill = `Fecha de maduración`), position = 'stack') +
# 
#   xlab('Fecha de maduración') +
#   ylab('Tasas spot') +
#   ggtitle('Distribución de las tasa spot') +
#   theme_minimal() +
#   theme(legend.position="none")
```



```r
ggplot(data = Datosgra10Y, aes(x =`Fecha de maduración` , y = Obtenido, group=`Fecha de maduración`)) + geom_boxplot(aes(color = `Fecha de maduración`), alpha = 0.7) + 
  geom_jitter(aes(color = `Fecha de maduración`), size = 1, alpha = 0.02)+
  #geom_violin(aes(fill = `Fecha de maduración`), color = 'black', alpha = 0.8)+
  scale_color_discrete(labels=c("1 mes", "6 meses", "1 año", "2 años", "3 años","5 años","7 años", "10 años","20 años","30 años"))+
  xlab('Fecha de maduración') + 
  ylab('Tasas spot en %') +
  ggtitle('Distribución de las tasa spot') + 
  theme_minimal()
```

![](LABORATORIO2_files/figure-latex/unnamed-chunk-6-1.pdf)<!-- --> 

Desviación estanda




```r
Datosgra1Y<-gather(datos1Y, "Fecha de maduración", Obtenido, names(datos1Y[2]):names(datos1Y[length(datos1Y)]))

ggplot(data = Datosgra1Y, aes(x =`Fecha de maduración` , y = Obtenido, group=`Fecha de maduración`)) + geom_boxplot(aes(color = `Fecha de maduración`), alpha = 0.7) + 
  geom_jitter(aes(color = `Fecha de maduración`), size = 1, alpha = 0.04)+
  #geom_violin(aes(fill = `Fecha de maduración`), color = 'black', alpha = 0.8)+
  scale_color_discrete(labels=c("1 mes", "6 meses", "1 año", "2 años", "3 años","5 años","7 años", "10 años","20 años","30 años"))+
  xlab('Fecha de maduración') + 
  ylab('Tasas spot en %') +
  ggtitle('Distribución de las tasa spot') + 
  theme_minimal()
```

![](LABORATORIO2_files/figure-latex/unnamed-chunk-7-1.pdf)<!-- --> 



```r
Datosgra1Mo<-gather(datos1Mo, "Fecha de maduración", Obtenido, names(datos1Mo[2]):names(datos1Mo[length(datos1Mo)]))

ggplot(data = Datosgra1Mo, aes(x =`Fecha de maduración` , y = Obtenido, group=`Fecha de maduración`)) + geom_boxplot(aes(color = `Fecha de maduración`), alpha = 0.7) + 
  geom_jitter(aes(color = `Fecha de maduración`), size = 1, alpha = 0.02)+
  scale_color_discrete(labels=c("1 mes", "6 meses", "1 año", "2 año", "3 año","5 año","7 año", "10 año","20 año","30 año"))+
  xlab('Fecha de maduración') + 
  ylab('Tasas spot en %') +
  ggtitle('Distribución de las tasa spot') + 
  theme_minimal()
```

![](LABORATORIO2_files/figure-latex/unnamed-chunk-8-1.pdf)<!-- --> 




Descripcion de lo de la pandemia







\begin{table}[H]

\caption{\label{tab:unnamed-chunk-9}Ejemplo de formato para tabla}
\centering
\begin{tabular}[t]{c}
\toprule
x\\
\midrule
1\\
2\\
3\\
4\\
5\\
\addlinespace
6\\
\bottomrule
\end{tabular}
\end{table}

\chapter{Metodología 1}
Cómo implementa la teoría expuesta en el marco teórico con sus datos, colocaremos aquí los resultados que se vayan obteniendo, incluir al menos un gráfico.


![](LABORATORIO2_files/figure-latex/unnamed-chunk-10-1.pdf)<!-- --> ![](LABORATORIO2_files/figure-latex/unnamed-chunk-10-2.pdf)<!-- --> ![](LABORATORIO2_files/figure-latex/unnamed-chunk-10-3.pdf)<!-- --> 



\chapter{Conclusiones y recomendaciones 1}



\chapter{Referencias bibliográficas}
\nocite{*}
\printbibliography

\chapter{Anexos}





