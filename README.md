# consultas-sql-en-base-de-datos-sqflite
Como hacer consultas sql cuando creas tu base de datos con sqflite, que tipo de datos asignar a las fechas

en la base de datos lo declaras como tipo integer.
en el modelo como tipo int.
para la consulta lo puedes manejar como string o como int.
puedes pasar de int a string, de string a DateTime,de DateTime a String y de String a int.
es decir lo puedes tener en la forma que desees, dependiendo si es para mostrarlo, o para c}hacer la consulta.
para poder hacer consultas de rango de fechas, debes manejarlas como tipo int, dandoles el siguiente formato: fecha = DateFormat('yyyyMMdd').format(picked);


  Future<List<CostoModel>> costosFiltrados(String fkidCultivo, String fechaDesde, String fechaHasta, String fkidproAct, String fkidConcepto) async {
   final res = await db.rawQuery('''

        SELECT * FROM Costos WHERE fkidProductoActividad IN (SELECT idProductoActividad FROM ProductosActividades WHERE fkidConcepto = '$fkidConcepto') AND fkidCultivo =          '$fkidCultivo' AND fkidProductoActividad = '$fkidproAct' AND fecha  BETWEEN '$fechaDesde' AND '$fechaHasta'
      
      ''');
      
    return res.isNotEmpty
      ? res.map((s) => CostoModel.fromJson(s)).toList()
      : [];
  
  }
} 
