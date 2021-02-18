# Modificar-estilos-de-excel-Datatable

```javascript
var table = $('#tabla_1').DataTable({
			dom: 'Bfrtip',
			buttons: [
				// { extend: 'copy', text: '<i class="fa fa-copy"></i> Copiar' },
				{ extend: 'csv', text: '<i class="fa fa-file-excel-o"></i> CSV',title: reportTitle(), },
				{ extend: 'excel',
					text: '<i class="fa fa-file-excel-o"></i> Excel',
					title: reportTitle(),
					customize: function(xlsx) {
						window.sheet = xlsx.xl.worksheets['sheet1.xml'];
						xlsx.xl['styles.xml'] = $.parseXML( banExcelStrings['xl/styles.xml'] );

    					$($(sheet).find('t')).each(function(k,v){
							if("pesimo" == $(v).text()) $(v).closest('c[t="inlineStr"]').attr('s',5);
							if("malo" == $(v).text()) $(v).closest('c[t="inlineStr"]').attr('s',5);
							if("medio" == $(v).text()) $(v).closest('c[t="inlineStr"]').attr('s',10);
							if("bueno" == $(v).text()) $(v).closest('c[t="inlineStr"]').attr('s',15);
							if("excelente" == $(v).text()) $(v).closest('c[t="inlineStr"]').attr('s',20);
						});
					}
				},
				{ extend: 'pdf', orientation: 'landscape', pageSize: 'A1', 
					text: '<i class="fa fa-file-pdf-o"></i> PDF', 
					title: reportTitle(),
					customize: function(doc) {
						for (var x = 3; x <= 19; x++) {
							text = table.column(x).data().toArray();
							//console.log(text);
							
							for (var i = 0; i < text.length; i++) {
								console.log(semaforoText(text[i]));
								doc.content[1].table.body[i+1][x].fillColor = semaforoText(text[i]);
							}
						}
					}
				},
				{ extend: 'print', text: '<i class="fa fa-print"></i> Imprimir',title: reportTitle(), },
				// 'copy', 'csv', 'excel', 'pdf', 'print'
			],
			ordering: false,
			scrollX: true,
			// scrollY:        "50vh",
			scrollCollapse: true,
			// paging:         false,
			fixedColumns:   {
				leftColumns: 1,
			},
			fixedHeader: true,
			scrollY:        "50vh",
			autoWidth : false
		});
	}
