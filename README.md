//SNEIDER SANCHEZ
/*Los objetos de este proyecto se pueden ejecutar en sus propios hilos gracias al metodo runable
esto significa que un objeto de tipo MiHilo es adecuado para usar como un hilo y se puede pasar al
constructor de Thread.*/

//crear una clase que implemente Runnable
 class MiHilo implements Runnable {
    String nombreHilo;

    MiHilo(String nombre){
        nombreHilo=nombre;
    }
    //Punto de entrada del hilo
    //Los hilos comienzan a ejecutarse aquí
    @Override
    public void run(){
        System.out.println("Comenzando "+nombreHilo);
        try {
            //se establece un bucle que cuenta de 0 a 9
            for (int contar=0; contar<10; contar++){
                /*sleep pausa el hilo durante 400 milisegundos cada vez a través del bucle.
                El retardo total dentro del bucle run() es de solo 4 segundos (10 iteraciones
                por 400 milisegundos)*/
                Thread.sleep(400);
                System.out.println("En "+nombreHilo+", el recuento "+contar);
            }
        }catch (InterruptedException exc){
            System.out.println(nombreHilo + "Interrumpido.");
        }
        //Se muestra en consola cada iteracion
        System.out.println("Terminando "+nombreHilo);
    }
}
class UsoHilos{
    public static void main(String[] args) {
        //Se muestra en consola el inicio de el hilo principal
        System.out.println("Hilo principal iniciando.");

        //Primero, se construye un objeto MiHilo que se usa para construir un objeto Thread.
        MiHilo mh=new MiHilo("HILO #1");

        //Luego se construye un hilo de ese objeto.
        Thread nuevoh=new Thread(mh);

        //Llamando a start se inicia la ejecucion del nuevo hilo.
        nuevoh.start();
        //Esto hace que comience el método run del hilo hijo.
        
        //Después de llamar a start, la ejecución vuelve a main, y entra main para el ciclo
        
        //Este ciclo itera 30 veces, pausando 5000 milisegundos cada vez
        for (int i=0; i<30;i++){
            System.out.print(" .");
        }try{
            Thread.sleep(5000);
        }catch (InterruptedException exc){
            System.out.println("Hilo principal interrumpido.");
        }
        //Se muestra en consola que ya ha finalizado el hilo principal MiHilo
        System.out.println("Hilo principal finalizado.");
        /*el hilo main y mh se ejecutan simultáneamente, es necesario evitar que main 
        termine hasta que termine mh.*/
    }
}
