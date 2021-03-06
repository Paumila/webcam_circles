# Definició de The Hough Transform

La definició de Hough transform es una eina que s'utilitza en el sistema de "computer vision" per analitzar imatges i processar imatges digitals. L'objectiu d'aquesta eina es trobar objectes amb clases de formes pero que són imperfectes. Gracies a uns parametres d'aquests algoritmes podem localitzar diferents formes en una imatge i poder-les dibuixar.

Aquesta funció va començar per poder detectar línies a imatges però ja s'ha ampliat a més formes arbitraries com el cercle, el·lipsis.

Una altre definició important és la de GaussianBlur que consisteix en una eina de filtratge del soroll. Es una eina per poder tractar les imatges per despres poder ser processades amb altres comandes. En aquest cas es filtra de soroll la imatge per poder eliminar possibles cercles falsos.

Les comandes que s'han utilitzat són:

```cv::HoughCircles( gray_image, circles, CV_HOUGH_GRADIENT, HOUGH_ACCUM_RESOLUTION, MIN_CIRCLE_DIST, CANNY_EDGE_TH, HOUGH_ACCUM_TH, MIN_RADIUS, MAX_RADIUS );```

Definició de cada parametre del HoughCircles (Anglès):

•	gray_image: Input image (grayscale)
•	circles: A vector that stores sets of 3 values: for each detected circle.
•	CV_HOUGH_GRADIENT: Define the detection method. Currently this is the only one available in OpenCV
•	HOUGH_ACCUM_RESOLUTION: The inverse ratio of resolution
•	MIN_CIRCLE_DIST = gray_image.rows/8: Minimum distance between detected centers
•	CANNY_EDGE_TH = 200: Upper threshold for the internal Canny edge detector
•	HOUGH_ACCUM_TH = 100*: Threshold for center detection.
•	MIN_RADIUS = 0: Minimum radio to be detected
•	MAX_RADIUS = 20: Maximum radius to be detected.

```cv::GaussianBlur( gray_image, gray_image, cv::Size(GAUSSIAN_BLUR_SIZE, GAUSSIAN_BLUR_SIZE), GAUSSIAN_BLUR_SIGMA );```

# Webcam_circles program

Detecció de cercles en la webcam del PC i mostrar aquests cercles en la imatge de la webcam.


Entrem en el nostre Github i fem un "fork" d'aquest Github https://github.com/beta-robots/webcam_circles.git

Clonem aquest repositori a la carpeta que nosaltres volguem del nostre ordinador

Un cop creat la nostre carpeta de treball comencem a realitzar modificacions en el programa

Executem el programa per veure que funciona i comprovem que no engega la webcam. Mirem en el programa i veiem que la última linia per tancar la finestra està configurada malament.

Modifiquem la linia de tancament de la finestra:

```if((cv::waitKey(1)) <= 0) break;```
```if((unsigned char)(cv::waitKey(1)) == 'q') break;```

Tornem a executar el programa i comprovem que funciona. Observem que en la imatge detecta molts cercles que son falsos

Modifiquem parametres per veure si podem reduir aquests cercles falsos

Primer de tot intentem modificar el filtre de soroll (GaussianBlur)

```cv::GaussianBlur( gray_image, gray_image, cv::Size(GAUSSIAN_BLUR_SIZE, GAUSSIAN_BLUR_SIZE), GAUSSIAN_BLUR_SIGMA );```

Canviem els valors de Gaussian_Blur_Size i el Gaussian_Blur_Sigma

Possem els valors més alts que els actuals i observem que al executar ens salta un error

Provem de possar els valors més baixos i observem que encara detecta més cercles falsos

Tornem a deixar les valors principals i intentem reduir els cercles falsos mirjançant la reducció de radi

La següent modificació consisteix en possar el Max_Radi a 20mm d'aquesta manera practicament només detectara monedes de tamany petit

```cv::HoughCircles( gray_image, circles, CV_HOUGH_GRADIENT, HOUGH_ACCUM_RESOLUTION, MIN_CIRCLE_DIST, CANNY_EDGE_TH, HOUGH_ACCUM_TH, MIN_RADIUS, MAX_RADIUS );```

Realitzan aquesta modificació aconseguim la reducció dels cercles falsos tot i que alguna moneda superior als 2cm la detecta. Suposem que al no saber quina distancia de la camera està col·locada la moneda de 50 centims potser la veu com una moneda de menys de 20mm

La última modificació que fem es canviar el punt del centre del cercle de color verd

```cv::circle(image, center, 3, cv::Scalar(0,255,0), -1, 8, 0 );```

# Used References

Aqui adjuntem les principals referencies que hem utilitzat per poder realitzar aquesta modificació en el programa webcam_point_features

<ol>
  
<li>https://docs.opencv.org/2.4/doc/tutorials/imgproc/gausian_median_blur_bilateral_filter/gausian_median_blur_bilateral_filter.html</li>

<li>https://docs.opencv.org/2.4/doc/tutorials/imgproc/imgtrans/hough_circle/hough_circle.html</li>

<li>https://en.wikipedia.org/wiki/Hough_transform</li>


</ol>

