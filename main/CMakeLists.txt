# Registrar los archivos fuente de la aplicacion principal
idf_component_register(
    SRCS 
        "main.cpp"
        "BluetoothHFP.cpp"
        "RadioNRF24.cpp"
    INCLUDE_DIRS 
        "."
    REQUIRES 
        "bt"    # Cargua la libreria nativa de Bluetooth
)
