// Función para determinar el número de carriles en función del tipo de vial
function setLanes(ROADS, type) {
    switch(type) {
        case 'Avenida':
        case 'Boulevard':
            ROADS.LANES_BACKWARD = 2;
            ROADS.LANES_FORWARD = 2;
            break;
        case 2:
            ROADS.LANES_BACKWARD = 1;
            ROADS.LANES_FORWARD = 1;
            break;
        default:
            console.log('Tipo de vial no reconocido');
    }
}

// Función principal de procesamiento
function Process(SOURCE, ROADS) {
    // Asignar valores a las propiedades de ROADS
    ROADS.EXTERNAL_ID = SOURCE["FeatId"];
    ROADS.MANUAL_STYLE = 'street/'+SOURCE["TIPOVIAL"];
    ROADS.NAME = SOURCE["NOMVIAL"];

    if (SOURCE["SENTIDO"] == "Dos sentidos") {
        ROADS.LANES_BACKWARD = 1;
        ROADS.LANES_FORWARD = 1;
    } else {
        ROADS.LANES_BACKWARD = 0;
        ROADS.LANES_FORWARD = SOURCE["TIPOSEN"];
    }

    // Llamar a la función setLanes para determinar el número de carriles
    setLanes(ROADS, SOURCE["TIPOVIAL"]);

    return true;
}