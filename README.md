# campeonato

package campeonatojava;
public class CampeonatoJava {

      public static void main(String[] args) {
        Time t[] = new Time[8];
      t[0] =  new Time ("Bragantino", 1,2,2,"D",8,true);
      t[1] =  new Time ("Caldense", 3,1,2,"D",7,true);
      t[2]= new Time ("Branquinhos", 3,2,1,"C",6,true);
      t[3] =  new Time ("Verdinhos", 2,2,1,"C",5,true);
      t[4] =  new Time ("Amareloes", 1,2,3,"B",4,true);
      t[5] =  new Time ("Misticos", 4,1,0,"B",3,true);
      t[6] =  new Time ("Bombom", 4,0,1,"A",2,true);
      t[7] =  new Time ("Canhoes", 5,0,0,"A",1,true);

   Partida UEC01 = new Partida(t[0],t[1],true);
   UEC01.marcarPartida(t[0], t[1]);
   t[0].status();
   t[1].status();

   UEC01.jogar();



    }

}


//classe Time

package campeonatojava;


public class Time implements Classificacao {
    private String nome;
    private int vitorias;
    private int derrotas;
    private int empates;
    private String grupo;
    private int posicaoAtual;
    private boolean classificado;

    public Time(String nome, int vitorias, int derrotas, int empates, String grupo, int posicaoAtual, boolean classificado) {
        this.nome = nome;
        this.vitorias = vitorias;
       this.derrotas = derrotas;
        this.empates = empates;
        this.grupo = grupo;
        this.posicaoAtual = posicaoAtual;
        this.classificado = classificado;
    }


    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getVitorias() {
        return vitorias;
    }

    public void setVitorias(int vitorias) {
        this.vitorias = vitorias;
    }


    public int getDerrotas() {
        return derrotas;
    }

    public void setDerrotas(int derrotas) {
        this.derrotas = derrotas;
    }

    public int getEmpates() {
        return empates;
    }

    public void setEmpates(int empates) {
        this.empates = empates;
    }

    public String getGrupo() {
        return grupo;
    }

    public void setGrupo(String grupo) {
        this.grupo = grupo;
    }

    public boolean getClassificado() {
        return classificado;
    }

    public void setClassificado(boolean classificado) {
        this.classificado = classificado;
    } 

    public int getPosicaoAtual() {
        return posicaoAtual;
    }

    public void setPosicaoAtual(int posicaoAtual) {
        this.posicaoAtual = posicaoAtual;
    }

    public void status(){
        System.out.println("_____________");
        System.out.println(" Hoje tem jogão de BOla no Estadio da Bananeiras ");
        System.out.println(" Primeiro Jogo temos " + this.getNome() + "\n Com " + 
                this.getVitorias() + " vitorias " + this.getEmpates()+" empates "+
                this.getDerrotas() + " derrotas ");
    }


       public void jogar(){
        this.classificado = true;

    }
    public void ganharJogo(){
        this.vitorias = this.vitorias+1;

    }public void perderJogo(){
        this.derrotas = this.derrotas+1;
    }
    public void empatarJogo(){
        this.empates  = this.empates +1;
     }

    @Override
    public void classificarTime() {
        this.classificado=true;
    }

    @Override
    public void desclassificar() {
        this.classificado = false;
    }

    @Override
    public void subirPosicao() {
        this.setVitorias(this.getVitorias()+1);
    }

    @Override
    public void descerPosicao() {
        this.setDerrotas(this.getDerrotas()+1);
    }

    @Override
    public void classLibertadores() {
        if(this.posicaoAtual <= 4){
            System.out.println(" Classificado para Libertadores  ");

        }else{
            System.out.println(" Não foi desssa vez, voce não foi pra Libertadores.");
        }
    }

    @Override
    public void classSulamericana() {
        if(this.posicaoAtual<=6){
            System.out.println(" Voce esta na Copa Sulamericanas ");

        }else {
            System.out.println(" Voce esta na zona de Rebaixamneto ");
        }
    }
   }




// classe Partida
package campeonatojava;

import java.util.Random;

public class Partida {
    private Time visitante;
    private Time daCasa;
    private boolean classificado;

    public Partida(Time daCasa, Time visitante,  boolean classificado) {
        this.daCasa = daCasa;
        this.visitante = visitante;
        this.classificado = classificado;
    }

    public Time getDaCasa() {
        return daCasa;
    }

    public void setDaCasa(Time daCasa) {
        this.daCasa = daCasa;
    }

    public Time getVisitante() {
        return visitante;
    }

    public void setVisitante(Time visitante) {
        this.visitante = visitante;
    }




    public boolean isClassificado() {
        return classificado;
    }

    public void setClassificado(boolean classificado) {
        this.classificado = classificado;
    }


    public void marcarPartida(Time t1, Time t2){
        if (t1.getGrupo().equals(t2.getGrupo())&& t1!=t2){
        this.classificado  = true;
        this.daCasa = t1;
        this.visitante = t2;

    } else {
        this.classificado = false;
        this.daCasa = null;
        this.visitante = null;
    }
    }
    public void jogar(){
       if(classificado){
           System.out.println("Bola rolando no Estadio do Bananeiras ");
           System.out.println( "Com os times " + daCasa.getNome() + "\n enfretando " + visitante.getNome());
           Random aleatorio = new Random ();
             int vencedor = aleatorio.nextInt(3);//0,1,2                 
       switch (vencedor){
           case 0:
               System.out.println("Jogo terminou empatado ");
               this.daCasa.empatarJogo();
               this.visitante.empatarJogo();
               break;

                case 1:
               System.out.println(" Vitoria de " + daCasa.getNome());
               this.daCasa.ganharJogo();
               this.visitante.perderJogo();
               break;

                case 2:
               System.out.println("Dessa vez, nao deu para " + daCasa.getNome() + "\n a vitoria de " +visitante.getNome());
               this.daCasa.perderJogo();
               this.visitante.ganharJogo();
               break;

       }
       }else{
           System.out.println("O jogo foi cancelado!!!!");
       }
}
}

        // interface Classificacao

    package campeonatojava;

public interface Classificacao {
    public void classificarTime();
    public void desclassificar();
    public void subirPosicao();
    public void descerPosicao();
    public void classLibertadores();
    public void classSulamericana();
}
