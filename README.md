<HEAD>
<style>
a.{text-decoration:none;color=blue}
a:visited{text-decoration:none;color=blue}
</style>

<script language="Html">
  
  var b=0;
DiaEnlace = new Array();

//################################################## ############
// formato para los enlaces
// DiaEnlace[b] = new Array(Mes,Dia,Url,Ventana);b++;

DiaEnlace[b] = new Array(12,10,"www.elcorteingles.es","_blank");b++;


var ns6=document.getElementById&&!document.all
var ie4=document.all

var ColorFondoCal = "#F8D3D3";
var ColorBordeCal = "white";
var ColorFondoCab = "#F8D3D3";
var ColorBordeCab = "white";
var ColorFondoDias = "#F5C5C5";
var ColorBordeDias = "white";
var ColorFondoActual = "Red";
var ColorTextDias = "Black";
var ColorTextActual = "Blue";
var FuenteDias = "Verdana; Arial";
  
var DiasPorMes = new Array(31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31);
var NombreMes = new Array('Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre');
var NombreDias = new Array('Lu', 'Ma', 'Mi', 'Ju', 'Vi', 'Sa', 'Do');
var MesSeleccionado;
var AnioSeleccionado;
var FechaActual = new Date();
var Hoy = FechaActual.getDate();
var MesActual = FechaActual.getMonth();
var AnioActual = FechaActual.getYear();
if (AnioActual < 1000)
AnioActual+=1900;
var startspaces=0;
                      
function Header(Year, Mes)
{
if (Mes == 1)
DiasPorMes[1] = ((Year % 400 == 0) || ((Year % 4 == 0) && (Year % 100 !=0))) ? 29 : 28;
var Header_String = NombreMes[Mes] + ' ' + Year;
return Header_String;
}
                      
function CreaCalendario(Year, Mes)
{

var PrimeraFecha = new Date(Year, Mes);
var Heading = Header(Year, Mes);
var PrimerDia = PrimeraFecha.getDay() ;

startspaces=Hoy;

while (startspaces > 7)
startspaces-=7;

startspaces = PrimerDia - 1;

if (startspaces < 0)
startspaces+=7;

var Cadena = '<table><font face="'+FuenteDias+'"><tr><td valign="top"><table BORDER=0 CELLSPACING=1 cellpadding=2 FRAME="box" BGCOLOR="'+ColorFondoCal+'" BORDERCOLORLIGHT="'+ColorBordeCal+'" bordercolordark="'+ColorBordeCal+'">';
Cadena += '<tr><th colspan=7 BGCOLOR="'+ColorFondoCab+'" BORDERCOLOR="'+ColorBordeCab+'">' + Heading + '</th></tr><tr>';
for (var j=0; j<7; j++)
{
Cadena += '<th ALIGN="CENTER" BGCOLOR="'+ColorFondoCab+'" BORDERCOLOR="'+ColorBordeCab+'">'+NombreDias[j]+'</th>'
}
Cadena += '<tr>';

for (s=0;s<startspaces;s++)
Cadena+="<td> </td>";

count=1;

while (count <= DiasPorMes[Mes])
{ for (b = startspaces;b<7;b++)
{ linktrue=false;

if (count==Hoy)
Cadena+="<td bgcolor='"+ColorFondoActual+"'><strong><center>";
else
Cadena+="<td><center>";

for (c=0;c<DiaEnlace.length;c++)
{ if ((DiaEnlace[c] != null) && (DiaEnlace[c][0]==Mes + 1) && (DiaEnlace[c][1]==count))
{ Cadena+='<a href="http://' + DiaEnlace[c][2] + '" target="'+DiaEnlace[c][3]+'" style="text-decoration=none" >';
linktrue=true;
}
}

if (count <= DiasPorMes[Mes])
Cadena+=count;
else
Cadena+="";

if (linktrue)
Cadena+="</a>";

if (count==Hoy)
Cadena+="</strong>";

Cadena+="</center></td>";
count++;
}
Cadena+="</tr><tr>";
startspaces=0;
}
Cadena += '</table></td></tr></table>';
cross_el=ns6? document.getElementById("Calendar") : document.all.Calendar
cross_el.innerHTML = Cadena;
}


function VerifFecha()
{ if ((event.keyCode < 48) || (event.keyCode > 57))
{ return false;
}
}

function On_Year()
{ var Year = document.when.anio.value;
if (Year.length == 4)
{ MesSeleccionado = document.when.Mes.selectedIndex;
AnioSeleccionado = Year;
CreaCalendario(AnioSeleccionado, MesSeleccionado);
}
}

function On_Mes()
{ var Year = document.when.anio.value;
if (Year.length == 4)
{ MesSeleccionado = document.when.Mes.selectedIndex;
AnioSeleccionado = Year;
CreaCalendario(AnioSeleccionado, MesSeleccionado);
}
else
{ alert('Año erroneo.');
document.when.anio.focus();
}
}


function PorDefecto() {
if (!ie4&&!ns6)
return
var Mid_Screen = Math.round(document.body.clientWidth / 2);
document.when.Mes.selectedIndex = MesActual;
document.when.anio.value = AnioActual;
MesSeleccionado = MesActual;
AnioSeleccionado = AnioActual;
CreaCalendario(AnioActual, MesActual);
}

function Pasar(direccion)
{ if (direccion == '+')
{ MesSeleccionado++;
if (MesSeleccionado == 12)
{ MesSeleccionado = 0;
AnioSeleccionado++;
}
}


if (direccion == '-')
{ MesSeleccionado--;
if (MesSeleccionado < 0)
{ MesSeleccionado = 11;
AnioSeleccionado--;
}
}

CreaCalendario(AnioSeleccionado, MesSeleccionado);
document.when.Mes.selectedIndex = MesSeleccionado;
document.when.anio.value = AnioSeleccionado;
}

</script>
</HEAD>

<body onLoad="PorDefecto()">
<div id=NavBar style="position: relative; width: 105; top: 5px; height: 24" align="left">
<form name="when">
<table width="51" >
<tr>
<td width="9" onClick="Pasar('-')"><</td>
<td width="1">
<select name="Mes" onChange="On_Mes()" style="font-size: 3 mm">
<script language="JavaScript1.2">
if (ie4||ns6)
{ for (j=0;j<NombreMes.length;j++)
{ document.writeln('<option value=' + j + ' style="font-size: 3 mm">' + NombreMes[j]);
}
}
</script>
</select>
</td>
<td width="1"><input type="text" name="anio" size=3 maxlength=4 onKeyPress="return VerifFecha()" onKeyUp="On_Year()" style="font-size: 3 mm"></td>
<td width="3" onClick="Pasar('+')">></td>
</tr>
</table>
</form>
</div>
<div id=Calendar style="position: relative; width: 76; top: -20px; height: 19" align="left"></div>
</BODY>  
                      

