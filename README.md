# counter-app
 counter app created using html tailwind and js

DATA: lv_order_number TYPE BAPI_ALM_ORDER_HEADER_E-ORDERID,
      ls_header       TYPE BAPI_ALM_ORDER_HEADER_E,
      lt_operations   TYPE TABLE OF BAPI_ALM_ORDER_OPERATION_E,
      lt_components   TYPE TABLE OF BAPI_ALM_ORDER_COMPONENT_E,
      lt_partner      TYPE TABLE OF BAPI_ALM_ORDER_PARTNER,
      lt_return       TYPE TABLE OF BAPIRET2.

lv_order_number = '000010000123'. "Example order number; replace with your order

CALL FUNCTION 'BAPI_ALM_ORDER_GET_DETAIL'
  EXPORTING
    number            = lv_order_number
  IMPORTING
    es_header         = ls_header
  TABLES
    et_operations     = lt_operations
    et_components     = lt_components
    et_partner        = lt_partner
    return            = lt_return.

* Display header data
WRITE: / 'Order:', ls_header-orderid,
         'Description:', ls_header-short_text,
         'Status:', ls_header-sys_status.

* Display operations
LOOP AT lt_operations INTO DATA(ls_op).
  WRITE: / 'Operation:', ls_op-activity, ' - ', ls_op-description.
ENDLOOP.

* Display components
LOOP AT lt_components INTO DATA(ls_comp).
  WRITE: / 'Component:', ls_comp-material, 'Qty:', ls_comp-quantity.
ENDLOOP.

* Handle return messages
LOOP AT lt_return INTO DATA(ls_ret).
  WRITE: / 'Message:', ls_ret-message.
ENDLOOP.


Frecuencia: [Frecuency]	Puesto de trabajo: [Work Center Desc]	 
Ultimo mtto prev: [Fecha Ultimo prev]	Tiempo Estimado: [Estimated Time Work]	
Ubicación Técnica: [Function Location]	Requerido por: [Planner Desc]	
Area de empresa: [Area Description]	No. Revisión: [Rev]	

Op.	Máquina	Componente	MP / MT	Descripción de actividad	Tiempo		
010	CAPSTAN 1	TRANSMISION 1	MP	REVISE ESTRUCTURA	15		
	
PUNTO DE VERIFICACION: TRANSMISION DE CAPSTAN, 
ACCION A TOMAR: REVISE TORNILLERIA DE FIJACION DE LA ESTRUCTURA Y REVISE QUE SE ENCUENTRE EN BUEN ESTADO 
VALOR ESTÁNDAR: 16 lb/ft      IT: NA	
	
030	RECOCIDO 1	BANDA 1	MP	REVISAR TENSION DE BANDA	5	M60	

PUNTO DE VERIFICACION: BANDAS, 
ACCION A TOMAR: REVISE QUE TENGA BUENA TENSION DE ACUERDO CON LA IT, REPARAR ANOMALIAS.  
VALOR ESTÁNDAR: NA        IT: 9999 00 04 T001	

020	DANCER 1	POLEA GUIA 3	MP	REVISIÓN DE POLEA GUIA 3	10	DC55	
	
PUNTO DE VERIFICACIÓN: POLEA DE DANCER, ACCIÓN A TOMAR: GIRE LA POLEA LOCA Y PONGA LA MANO EN TRE LA FLECHA Y EL RODAMIENTO SI SE SIENTE RESECO O CON VIBRACION EN LA FLECHA ENTONCES REEMPLAZE EL RODAMIENTO, IT: 9999 00 04 T001	
030	RECOCIDO 1	BANDA 1	MP	REVISAR TENSION DE BANDA	25	GM60	
	
PUNTO DE VERIFICACION: BANDAS, ACCION A TOMAR: REVISE QUE TENGA BUENA TENSION DE ACUERDO CON LA IT, REPARAR ANOMALIAS. IT: 9999 00 04 T001	

Observaciones ____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

Op.	Material	Descripción	Cantidad	UM	Sol. Pedido	Reserva
020	DC55	BALERO SKF 6000 2RS  	1	PZ	[Request Number]	[Reserva]
030	GM60	BANDA MARCA GATES TIPO V CX112  	[Quantity]	[Measure Unit]	[Request Number]	[Reserva]





En la parte posterior de la página llevará el siguiente contenido:

NOTAS IMPORTANTES:
 1. DESPUES DE MP DE LA MAQUINA EFECTUAR LIMPIEZA DEL AREA DE TRABAJO CON LA CORRECTA SEGREGACION DE RESIDUOS PELIGROSOS Y NO PELIGROSOS GENERADOS
2. REPORTAR CAUSA DE NO TERMINAR MP EN CASO DE NO TERMINARLO
3. CUALQUIER ACCION TOMADA (CAMBIO, AJUSTE, ALINEACION, ETC) DEBERA SER REPORTADA EN LA ORDEN DE TRABAJO DE MANTENIMIENTO PREVENTIVO
4. LLENE TODOS LOS CAMPOS DE LA OT DE MANERA CORRECTA
5. FIRMAR LA ORDEN POR TODO EL PERSONAL QUE ATENDIO EL MP

	MANTENIMIENTO			PRODUCCION
 	REALIZÓ TRABAJO			ACEPTO TRABAJO
FIRMA	 		FIRMA	 
NOMBRE	 		NOMBRE	 
				
			HORA INICIO DE MP	 
			HORA DE TERMINO DE MP	 
 

Formato Hoja de bloqueo y candadeo

En Viakable, como parte de nuestras medidas de seguridad durante la ejecución de trabajos de mantenimiento, utilizamos un formato impreso conocido como hoja de bloqueo/candadeo. Este documento cumple una función crítica en la prevención de accidentes laborales.

Su propósito principal es informar de manera visible y clara que una máquina se encuentra en mantenimiento activo, y que, por lo tanto, no debe ser encendida, operada ni manipulada en ninguna circunstancia.

La presencia de esta hoja en el equipo actúa como una señal de advertencia para todo el personal, reforzando el cumplimiento de los protocolos de seguridad y ayudando a evitar incidentes que puedan poner en riesgo la integridad de los trabajadores o dañar los equipos.

A continuación, se muestran los datos que se deberán imprimir en el formato, las etiquetas de datos deberán estar disponibles tanto en español como en inglés 

Nombre: Nombre del técnico.
Fecha de inicio: Fecha de inicio programada de la orden de mantenimiento
Hora de inicio: Hora de inicio programada de la orden de mantenimiento
Fecha de termino: Fecha de termino programada de la orden de mantenimiento
Hora de termino: Hora de termino programada de la orden de mantenimiento
Supervisor: Código y descripción del encargado del puesto de trabajo
Programador: Código y descripción del planeador del puesto de trabajo
Orden de trabajo: Clave o número de la orden de mantenimiento
Equipo o instalación: Número del equipo y descripción del equipo a mantener – Número y descripción del equipo superior
Ubicación Técnica: Código y descripción de la ubicación técnica
Descripción del trabajo: Descripción de la orden de mantenimiento 
TARJETA DE BLOQUEO Y CANDADEO
PROHIBIDO
No debe activarse la maquinaria o equipo, ni retirar la tarjeta de este lugar
 

Nombre:	[Nombre del técnico]
Fecha de inicio:	[Fecha de inicio del mantenimiento]
Hora de inicio:	[Hora de inicio del mantenimiento]
Fecha de término:	[Fecha de término del mantenimiento]
Hora de término:	[Hora de término del mantenimiento]
Supervisor:	[Nombre encargado del work center]
Programador:	[Nombre del programador de mtto]
Orden de trabajo:	[Número de orden de trabajo]
Equipo o instalación:	[Equipo a mantener] [Equipo superior]
Ubicación técnica:	[Clave y descripción de la ub técnica]
Descripción del trabajo:	[Descripción orden de mtto]

LISTA DE CONTROL H-A-C-E DE TOMADOS
Toma dos minutos de realizar cualquier actividad, piensa en seguridad, elimina todo que te puede causar daños a ti y a los demás. Empieza tu trabajo repasando la lista de control, H-A-C-E
Hablar	“¿He hablado con todos los interesados sobre lo que pretendo hacer y cómo podría afectar a terceros?”
“¿He hablado con las personas precisas sobre todo aquello que a mi parecer podría hacer más seguro mi trabajo?
Acciones	“¿En que forma mis acciones podrían afectar mi propia seguridad?”
“¿En que forma mis acciones podrían afectar la seguridad de otros?”
Conocimiento	“¿Conozco los procedimientos, tanto escritos como no escritos?”
“¿Estoy al tanto de todos los peligros de los alrededores y del medio ambiente y sé que hacer al respecto a cada uno de ellos?”
Equipo	“¿Cuento con equipo de protección adecuado/apropiado para este trabajo?”
“¿Tengo las herramientas y el equipo correcto para este trabajo concreto y están en buenas condiciones?”
TOMA DOS… y contesta sus preguntas

Frequency: [Frequency]	Job Title: [Work Center Desc]	 
Ultimo mtto prev: [Last Prev Date]	Estimated Time Work: [Estimated Time Work]	
Technical Location: [Function Location]	Required by: [Planner Desc]	
Company Area: [Area Description]	Revision No.: [rev]	

Op.	Machine	Component	MP/MT	Description of activity	Time		
010	CATCH 1	TRANSMISSION 1	MP	CHECK STRUCTURE	15		
	
CHECKPOINT: CAPTAN TRANSMISSION, 
ACTION TO TAKE: CHECK THE FIXING SCREWS OF THE STRUCTURE AND CHECK THAT IT IS IN GOOD CONDITION 
STANDARD VALUE: 16 lb/ft      IT: NA	
	
030	ANNEALING 1	BAND 1	MP	CHECK BELT TENSION	5	M60	

CHECKPOINT: BANDS, 
ACTION TO TAKE: CHECK THAT IT HAS GOOD TENSION ACCORDING TO THE IT, REPAIR ABNORMALITIES. 
STANDARD VALUE: NA IT: 9999 00 04 T001	

020	DANCER 1	GUIDE PULLEY 3	MP	GUIDE PULLEY OVERHAUL 3	10	DC55	
	
CHECK POINT: DANCER'S PULLEY, ACTION TO TAKE: TURN THE IDLER PULLEY AND PUT YOUR HAND BETWEEN THE ARROW AND THE BEARING IF YOU FEEL DRY OR VIBRATING IN THE ARROW THEN REPLACE THE BEARING, IT: 9999 00 04 T001	
030	ANNEALING 1	BAND 1	MP	CHECK BELT TENSION	25	GM60	
	
CHECKPOINT: BANDS, ACTION TO TAKE: CHECK THAT IT HAS GOOD TENSION ACCORDING TO THE IT, REPAIR ANOMALIES. IT: 9999 00 04 T001	

Remarks____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

Op.	Material	Description	Quantity	UM	Sun. Order	Reservation
020	DC55	SKF 6000 2RS BEARING	1	PZ	[Request Number]	[Reservation]
030	GM60	GATES V-TYPE CX112 BAND	[Quantity]	[Measure Unit]	[Request Number]	[Reservation]





On the back of the page you will have the following content:

IMPORTANT NOTES:
 1. AFTER MP OF THE MACHINE, CLEAN THE WORK AREA WITH THE CORRECT SEGREGATION OF HAZARDOUS AND NON-HAZARDOUS WASTE GENERATED
2. REPORT CAUSE OF NOT FINISHING MP IN CASE OF NOT FINISHING IT
3. ANY ACTION TAKEN (CHANGE, ADJUSTMENT, ALIGNMENT, ETC.) MUST BE REPORTED IN THE PREVENTIVE MAINTENANCE WORK ORDER
4. FILL IN ALL THE OT FIELDS CORRECTLY
5. SIGN THE ORDER FOR ALL THE PERSONNEL WHO ATTENDED THE MP

	MAINTENANCE			PRODUCTION
 	PERFORMED WORK			I ACCEPT WORK
SIGNATURE	 		SIGNATURE	 
NAME	 		NAME	 
				
			MP START TIME	 
			MP END TIME	 
 

Format Lock and lock sheet

At Viakable, as part of our safety measures during the execution of maintenance work, we use a printed format known as a lock/lock sheet. This document plays a critical role in the prevention of workplace accidents.

Its main purpose is to provide visible and clear information that a machine is under active maintenance, and therefore should not be switched on, operated or tampered with under any circumstances.

The presence of this sheet on the equipment acts as a warning sign for all personnel, reinforcing compliance with safety protocols and helping to avoid incidents that may put the integrity of workers at risk or damage the equipment.

Below are the data that must be printed in the format, the data labels must be available in both Spanish and English 

Name: Name of the technician.
Start Date: Scheduled Start Date of the Maintenance Order
Start Time: Scheduled start time of the maintenance order
End Date: Scheduled End Date of the Maintenance Order
End Time: Scheduled End Time of the Maintenance Order
Supervisor: Code and description of the person in charge of the job
Programmer: Code and description of the job planner
Work Order: Maintenance Order Key or Number
Equipment or installation: Equipment number and description of equipment to be maintained – Number and description of top equipment
Technical Location: Code and description of the technical location
Job Description: Maintenance Order Description 
LOCK AND LOCK CARD
FORBIDDEN
Machinery or equipment should not be activated, nor should the card be removed from this location
 

Name:	[Technician's Name]
Start date:	[Maintenance Start Date]
Start time:	[Maintenance Start Time]
End date:	[Maintenance End Date]
End time:	[Maintenance End Time]
Supervisor:	[Name in charge of the work center]
Programmer:	[MTTO Programmer's Name]
Work Order:	[Work Order Number]
Equipment or installation:	[Equipment to maintain] [Top Team]
Technical Location:	[Key and description of the technical ub]
Job Description:	[MTTO Order Description]

H-A-C-E CHECKLIST OF TAKEN
Take two minutes to do any activity, think about safety, eliminate everything that can cause harm to you and others. Start your work by going through the checklist, H-A-C-E
Speak	"Have I talked to all stakeholders about what I intend to do and how it might affect third parties?"
"Have I talked to the right people about everything that I think could make my job safer?
Actions	"How might my actions affect my own safety?"
"How might my actions affect the safety of others?"
Knowledge	"Do I know the procedures, both written and unwritten?"
"Am I aware of all the dangers of the surroundings and the environment and do I know what to do about each of them?"
Team	"Do I have adequate/appropriate protective equipment for this job?"
"Do I have the right tools and equipment for this particular job and are they in good condition?"
<00000><00001>
Um
<00002>
Quantity
<00003>
Time
<00004>
PRODUCTION
<00005>
MP/MT
<00006>
Frequency
<00007>
Technical Location :
<00008>
End Date :
<00009>
Last prev Date :
<00010>
Description Of Activity
<00011>
Sun.order
<00012>
Start date :
<00013>
Job Title :
<00014>
Material
<00015>
Start time :
<00016>
Name :
<00017>
Required by:
<00018>
Company Area :
<00019>
MP START TIME
<00020>
I ACCEPT WORK
<00021>
Job Description
<00022>
                     
<00023>
LOCK AND
<00024>
 
<00025>
LOCK CARD
<00026>
 
<00027>
FORBIDDEN
<00028>
Machinery or equipment should not be activated, nor should the card be removed from this location
<00029>
 
<00030>
                  
<00031>
Component
<00032>
1234567890
<00033>
Op.
<00034>
Estimated time Work :
<00035>
Work Order
<00036>
IMPORTANT NOTES:	
1. AFTER MP OF THE MACHINE, CLEAN THE WORK AREA WITH THE CORRECT SEGREGATION OF HAZARDOUS AND NON-HAZARDOUS WASTE GENERATED	
2. REPORT CAUSE OF NOT FINISHING MP IN CASE OF NOT FINISHING IT	
3. ANY ACTION TAKEN (CHANGE, ADJUSTMENT, ALIGNMENT, ETC.) MUST BE REPORTED IN THE PREVENTIVE MAINTENANCE WORK ORDER	
4. FILL IN ALL THE OT FIELDS CORRECTLY	
5. SIGN THE ORDER FOR ALL THE PERSONNEL WHO ATTENDED THE MP	
<00037>
No.Revision:
<00038>
             -
<00039>
SIGNATURE
<00040>
End time :
<00041>
Remarks _______________________________________________________________________________________________
_______________________________________________________________________________________________________
_______________________________________________________________________________________________________
<00042>
Op.
<00043>
Supervisor :
<00044>
NAME
<00045>
Reservation
<00046>
PERFORMED WORK
<00047>
 ---
<00048>
Material Description
<00049>
Equipment Number
<00050>
MAINTENANCE
<00051>
Programmer :
<00052>
  -
<00053>
NAME
<00054>
Machine
<00055>
SIGNATURE
<00056>
MP END TIME
<00057>
Technical Location
<00058>


