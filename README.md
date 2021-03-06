# Lab 02- BCD2SSEG
laboratorio 02 simulación

* Roberto 
* Diego


El siguiente documento tiene como fin exponer los conocimientos acerca del diseno de hardware atravez del lenguaje verilog, por consiguiente la siguiente es una reproduccion de la implementacion de un modulo que tiene entradas BCD  y convierto por asi decirlo en bit aptos para 7segmentos, la metodologia consiste en explicar un codigo proporcionado y siguiente a eso realizar las respectivas simulaciones.

#comprension del codigo HDL

```
module BCDtoSSeg (BCD, SSeg, an);   // asignacion del modulo con 3 parametros
                                    // BCD  corresponde a la entrada de 4 bits BCD
                                    // SSeg corresponde a la salida de siete segmentos
                                    // an corresponde a la salida de anodo, dado que todos los 
                                        7seg comparten el mismo bus hace falta turnarlos por medio de un mux


  input [3:0] BCD;                  // entrada BCD 4 bits
  output reg [0:6] SSeg;            // salida 7seg, ABCDEFG
  output [3:0] an;                  // salida la cual activa cada 7seg

assign an=4'b1110;                  // Dado que es anodo comun las salidas se dan en logica negativa 


always @ ( * ) begin
  case (BCD)
    4'b0000: SSeg = 7'b0000001; // "0"             equivalente en logica negativa
	4'b0001: SSeg = 7'b1001111; // "1" 
	4'b0010: SSeg = 7'b0010010; // "2" 
	4'b0011: SSeg = 7'b0000110; // "3" 
	4'b0100: SSeg = 7'b1001100; // "4" 
	4'b0101: SSeg = 7'b0100100; // "5" 
	4'b0110: SSeg = 7'b0100000; // "6" 
	4'b0111: SSeg = 7'b0001111; // "7" 
	4'b1000: SSeg = 7'b0000000; // "8"  
	4'b1001: SSeg = 7'b0000100; // "9" 
   4'ha: SSeg = 7'b0001000;  
   4'hb: SSeg = 7'b1100000;
   4'hc: SSeg = 7'b0110001;
   4'hd: SSeg = 7'b1000010;
   4'he: SSeg = 7'b0110000;
   4'hf: SSeg = 7'b0111000;
    default:
    SSeg = 0;
  endcase
end

endmodule

```


El siguiente es el archivo TB
```
`timescale 1ns / 1ps   //escala de tiempo en 1 pico segundo

module BCDtoSSeg_TB; //Declaracion del modulo
	// Inputs
	reg [3:0] BCD; //entrada BCD 4 bits
	// Outputs
	wire [6:0] SSeg; // salida 7 segmentos 7 bits

	//inicia la caja uut con los rastreadores de tiempo
	BCDtoSSeg uut (
	//aplica el tiempo en las terminales del modulo  BCDtoSSeg_TB
		.BCD(BCD), 
		.SSeg(SSeg)
	);

	initial begin
		// asigna 10 picosegundos a cada prueba bcd
		BCD = 0; #10;
		BCD = 1; #10;
		BCD = 2; #10;
		BCD = 3; #10;
		BCD = 4; #10;
		BCD = 5; #10;
		BCD = 6; #10;
		BCD = 7; #10;
		BCD = 8; #10;
		BCD = 9; #10;

	end

   initial begin: TEST_CASE
     $dumpfile("BCDtoSSeg_TB.vcd");
     #(200) $finish;
   end

endmodule

```
A continuacion la simulacion del archivo Techbench

![Simulacion BCDtoSSeg](https://github.com/unal-edigital1-lab/lab02-2021-2-grupo09-2021-2-/blob/master/imag/simulacion_archivos_dhl.PNG)

