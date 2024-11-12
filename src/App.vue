<template>
  <main
    class="columns is-gapless is-multiline"
    :class="{ 'modo-escuro': isModoEscuroActivo }"
  >
    <div class="column is-one-quarter">
      <BarraLateral @ao-tema-alterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioPrincipal @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <TarefaToDo
          v-for="(tarefa, index) in tarefas"
          :tarefa="tarefa"
          :key="index"
        />
        <BoxTask v-if="isListaVazia">
          Você não está muito produtivo hoje 😥
        </BoxTask>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue";
import FormularioPrincipal from "./components/FormularioPrincipal.vue";
import TarefaToDo from "./components/TarefaToDo.vue";
import ITarefa from "./Interfaces/ITarefa";
import BoxTask from "./components/BoxTask.vue";
import Smooch from "smooch";

export default defineComponent({
  name: "App",
  components: { BarraLateral, FormularioPrincipal, TarefaToDo, BoxTask },
  data() {
    return {
      tarefas: [] as ITarefa[],
      isModoEscuroActivo: false,
    };
  },
  computed: {
    isListaVazia(): boolean {
      return this.tarefas.length == 0;
    },
  },
  mounted() {
    this.initSmooch();
  },
  methods: {
    initSmooch() {
      const agent = 'B0CB8EFE-53E9-410C-837B-715CE6F47FA5' //  "b94571c2-1bd3-4ec1-8789-d939fa680f89"; //"788ce9ba-93e3-41a2-88bd-9bf2254c0ce8";
      const delegate = {
        beforeSend(message: any, data: any) {
          /* if (data.conversation.id === '<conversation-id>' && message.role === 'user') {
              message.metadata = {
                  ...message.metadata,
                  currentUrl: window.location.href
              };
          } */
          message.metadata = {
            ...message.metadata,
            agent,
          };
          return message;
        },
      };
      Smooch.init({
        delegate,
        integrationId:'5efb8d0407910c000c9c66a1', // [Auria]"62deaa89bc120d00efffef7a",
        menuItems: {
          imageUpload: false,
          fileUpload: false,
          shareLocation: false,
        },
         /*customColors: {
          brandColor: "1b79ae",
          conversationColor: "1b79ae",
          actionColor: "1b79ae",
        },*/

        customText: {
          syncConversation: "Sincronizar conversa",
          linkChannelPageHeader: "Sincronizar sua conversa",
          connectNotificationText:
            "Sincronize sua conversa e continue nos enviando mensagens através do seu aplicativo favorito.",
          viberChannelDescription:
            "Conecte sua conta do Viber para ser notificado quando receber uma resposta e continue a conversa no Viber. Para começar, digitalize o código QR usando o aplicativo Viber.",
          telegramChannelDescription:
            "Conecte sua conta do Telegram para ser notificado quando receber uma resposta e continuar a conversa no Telegram",
          messengerChannelDescription:
            "Conecte sua conta do Facebook Messenger para ser notificado quando receber uma resposta e continue a conversa no Facebook Messenger.",
          //Labels da caixa de envio
          headerText: "Posso ajudar?",
          inputPlaceholder: "Digite a mensagem...",
          sendButtonText: "Enviar",
          //Labels de Tempo
          conversationListTimestampFormat: "D/MM/YYYY",
          conversationTimestampHeaderFormat: "D/MM/YYYY, HH:MM",
          conversationListHeaderText: "Minhas Conversas",
          conversationListRelativeTimeJustNow: "Agora Mesmo!",
          conversationListPreviewUserText: "Você",
          conversationListRelativeTimeMinute: "1 minutos atrás",
          conversationListRelativeTimeMinutes: "{value} minutos atrás",
          conversationListRelativeTimeHour: "1 hora atrás",
          conversationListRelativeTimeHours: "{value} horas atrás",
          conversationListRelativeTimeYesterday: "Ontem",
          messageIndicatorTitlePlural: "({count}) Novas mensagens",
          messageIndicatorTitleSingular: "({count}) Nova mensagem",
          messageRelativeTimeDay: "{value}d atrás",
          messageRelativeTimeHour: "{value}h atrás",
          messageRelativeTimeJustNow: "Agora Mesmo!",
          messageRelativeTimeMinute: "{value}m atrás",
          messageTimestampFormat: "HH:MM",
          messageDelivered: "Entregue",
          messageSeen: "Visto",
          messageSending: "Enviando ...",
          newConversationButtonText: "Nova Conversa",
        },
        /* customColors: {
            brandColor: '65758e',
            conversationColor: '65758e',
            actionColor: '65758e',
        }, */
      });
    },
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroActivo: boolean) {
      this.isModoEscuroActivo = modoEscuroActivo;
    },
  },
});
</script>

<style>
.lista {
  padding: 1.25rem;
}

main {
  --bg-primario: #fff;
  --texto-primario: #1d1d1b;
}

main.modo-escuro {
  --bg-primario: #1d1d1b;
  --texto-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
}
</style>
