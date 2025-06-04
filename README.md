# WhatsApp-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Messaging App Like WhatsApp</title>
<style>
  :root {
    --primary-color: #128c7e;
    --primary-color-light: #25d366;
    --background-color: #ece5dd;
    --chat-background: #fff;
    --text-color: #222;
    --secondary-text-color: #777;
    --input-background: #f0f0f0;
    --input-text-color: #333;
    --border-color: #ddd;
    --message-sent-bg: #dcf8c6;
    --message-received-bg: #fff;
    --scrollbar-bg: #f1f1f1;
  }

  * {
    box-sizing: border-box;
  }

  body {
    margin:0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: var(--background-color);
    color: var(--text-color);
    height: 100vh;
    display: flex;
    overflow: hidden;
  }

  #app {
    display: flex;
    flex: 1;
    height: 100vh;
    max-height: 100vh;
  }

  /* Sidebar */
  #sidebar {
    width: 320px;
    background: #f8f9fa;
    border-right: 1px solid var(--border-color);
    display: flex;
    flex-direction: column;
  }

  #sidebar-header {
    padding: 15px 20px;
    background: var(--primary-color);
    color: white;
    font-size: 1.3rem;
    font-weight: 700;
    user-select: none;
  }

  #search-box {
    padding: 10px 20px;
    border-bottom: 1px solid var(--border-color);
  }

  #search-input {
    width: 100%;
    padding: 8px 10px;
    font-size: 1rem;
    border: 1px solid var(--border-color);
    border-radius: 20px;
    outline: none;
  }

  #contacts-list {
    overflow-y: auto;
    flex: 1;
    background: white;
  }

  .contact-item {
    display: flex;
    align-items: center;
    padding: 12px 20px;
    cursor: pointer;
    border-bottom: 1px solid var(--border-color);
    transition: background-color 0.15s ease;
  }
  .contact-item:hover,
  .contact-item.active {
    background-color: var(--primary-color-light);
    color: white;
  }

  .contact-avatar {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background-color: var(--primary-color);
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 700;
    font-size: 1.3rem;
    margin-right: 15px;
    flex-shrink: 0;
  }

  .contact-info {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }
  .contact-name {
    font-weight: 600;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
  }
  .contact-last-message {
    font-size: 0.875rem;
    color: var(--secondary-text-color);
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
  }

  /* Chat Area */
  #chat-area {
    flex: 1;
    display: flex;
    flex-direction: column;
    background: var(--chat-background);
  }

  #chat-header {
    height: 60px;
    background: var(--primary-color);
    color: white;
    display: flex;
    align-items: center;
    padding: 0 20px;
    font-weight: 700;
    font-size: 1.25rem;
    user-select: none;
  }

  #chat-messages {
    flex: 1;
    padding: 20px;
    overflow-y: auto;
    background-image: url('https://www.transparenttextures.com/patterns/diagmonds-light.png');
  }

  .message {
    max-width: 60%;
    padding: 10px 14px;
    margin-bottom: 12px;
    border-radius: 7px;
    position: relative;
    word-wrap: break-word;
    font-size: 1rem;
  }
  .message.sent {
    background-color: var(--message-sent-bg);
    margin-left: auto;
    border-bottom-right-radius: 0;
  }
  .message.received {
    background-color: var(--message-received-bg);
    margin-right: auto;
    border-bottom-left-radius: 0;
    border: 1px solid #ddd;
  }
  .message-time {
    font-size: 0.7rem;
    color: var(--secondary-text-color);
    position: absolute;
    bottom: 2px;
    right: 8px;
  }

  #chat-input-area {
    border-top: 1px solid var(--border-color);
    padding: 10px 20px;
    display: flex;
    align-items: center;
    background-color: var(--chat-background);
  }

  #chat-input {
    flex: 1;
    padding: 10px 14px;
    border-radius: 20px;
    border: 1px solid var(--border-color);
    font-size: 1rem;
    outline: none;
  }
  #send-button {
    background: var(--primary-color);
    color: white;
    border: none;
    margin-left: 12px;
    padding: 10px 16px;
    font-weight: 700;
    font-size: 1rem;
    border-radius: 20px;
    cursor: pointer;
    user-select: none;
    transition: background-color 0.2s ease;
  }
  #send-button:hover {
    background-color: var(--primary-color-light);
  }

  /* Scrollbar styling */
  #contacts-list::-webkit-scrollbar,
  #chat-messages::-webkit-scrollbar {
    width: 8px;
  }
  #contacts-list::-webkit-scrollbar-thumb,
  #chat-messages::-webkit-scrollbar-thumb {
    background-color: #bbb;
    border-radius: 4px;
  }
  #contacts-list::-webkit-scrollbar-track,
  #chat-messages::-webkit-scrollbar-track {
    background-color: var(--scrollbar-bg);
  }

  /* Responsive */
  @media (max-width: 700px) {
    #sidebar {
      width: 100%;
      height: 50vh;
      border-right: none;
      border-bottom: 1px solid var(--border-color);
    }
    #chat-area {
      height: 50vh;
    }
    body {
      flex-direction: column;
    }
  }
</style>
</head>
<body>
<div id="app" role="main" aria-label="Messaging app">
  <aside id="sidebar" aria-label="Contacts and search">
    <div id="sidebar-header">My Chats</div>
    <div id="search-box">
      <input type="search" id="search-input" placeholder="Search contacts..." aria-label="Search contacts"/>
    </div>
    <div id="contacts-list" tabindex="0" aria-live="polite" aria-relevant="additions removals"></div>
  </aside>
  <section id="chat-area" aria-label="Chat area">
    <header id="chat-header" aria-live="polite">
      Select a contact to chat
    </header>
    <div id="chat-messages" tabindex="0" aria-label="Messages"></div>
    <form id="chat-input-area" aria-label="Send message" onsubmit="return false;">
      <input
        type="text"
        id="chat-input"
        placeholder="Type a message"
        aria-label="Type a message"
        autocomplete="off"
        disabled
        />
      <button id="send-button" aria-label="Send message" disabled>Send</button>
    </form>
  </section>
</div>

<script>
  (() => {
    // Demo contacts list
    const contacts = [
      { id: 'alice', name: 'Alice Wonderland' },
      { id: 'bob', name: 'Bob Builder' },
      { id: 'carol', name: 'Carol Danvers' },
      { id: 'dave', name: 'Dave Grohl' },
      { id: 'eve', name: 'Eve Polastri' },
      { id: 'frank', name: 'Frank Castle' }
    ];

    // In memory current selected contact
    let currentContactId = null;

    // Elements
    const contactsListEl = document.getElementById('contacts-list');
    const chatHeaderEl = document.getElementById('chat-header');
    const chatMessagesEl = document.getElementById('chat-messages');
    const chatInputEl = document.getElementById('chat-input');
    const sendButtonEl = document.getElementById('send-button');
    const searchInputEl = document.getElementById('search-input');

    // Helper: Save messages in localStorage keyed by contact id
    function saveMessages(contactId, messages) {
      localStorage.setItem(`chat_messages_${contactId}`, JSON.stringify(messages));
    }

    function loadMessages(contactId) {
      const data = localStorage.getItem(`chat_messages_${contactId}`);
      return data ? JSON.parse(data) : [];
    }

    // Helper: format time HH:MM
    function formatTime(date) {
      const h = date.getHours().toString().padStart(2, '0');
      const m = date.getMinutes().toString().padStart(2, '0');
      return `${h}:${m}`;
    }

    // Create avatar text (initials)
    function avatarText(name) {
      return name.split(' ').map(part => part[0].toUpperCase()).join('').slice(0, 2);
    }

    // Update contact last message preview in contact list
    function updateContactLastMessage(contactId, lastMessageText) {
      const el = document.querySelector(`.contact-item[data-contact-id="${contactId}"] .contact-last-message`);
      if(el) el.textContent = lastMessageText;
    }

    // Render contacts filtered by search string
    function renderContacts(filter = '') {
      contactsListEl.innerHTML = '';
      const filterLc = filter.toLowerCase();

      const filtered = contacts.filter(c => c.name.toLowerCase().includes(filterLc));

      if (filtered.length === 0) {
        contactsListEl.innerHTML = '<p style="padding:15px; color:#999;">No contacts found.</p>';
        return;
      }

      filtered.forEach(contact => {
        // Get last message preview
        const messages = loadMessages(contact.id);
        const lastMessage = messages.length ? messages[messages.length - 1].text : '';
        const lastMsgShort = lastMessage.length > 30 ? lastMessage.slice(0, 27) + '...' : lastMessage;

        const contactEl = document.createElement('div');
        contactEl.className = 'contact-item';
        contactEl.tabIndex = 0;
        contactEl.setAttribute('data-contact-id', contact.id);
        contactEl.setAttribute('role', 'button');
        contactEl.setAttribute('aria-pressed', contact.id === currentContactId ? 'true' : 'false');
        contactEl.innerHTML = `
          <div class="contact-avatar" aria-hidden="true">${avatarText(contact.name)}</div>
          <div class="contact-info">
            <div class="contact-name">${contact.name}</div>
            <div class="contact-last-message">${lastMsgShort}</div>
          </div>
        `;
        if(contact.id === currentContactId) contactEl.classList.add('active');
        contactsListEl.appendChild(contactEl);
      });
    }

    // Render messages for a contact
    function renderMessages(contactId) {
      chatMessagesEl.innerHTML = '';
      if(!contactId) return;

      const messages = loadMessages(contactId);
      messages.forEach(msg => {
        const msgEl = document.createElement('div');
        msgEl.className = 'message ' + (msg.sentByMe ? 'sent' : 'received');
        msgEl.textContent = msg.text;

        const timeEl = document.createElement('div');
        timeEl.className = 'message-time';
        timeEl.textContent = formatTime(new Date(msg.timestamp));
        msgEl.appendChild(timeEl);

        chatMessagesEl.appendChild(msgEl);
      });
      // Scroll to bottom
      chatMessagesEl.scrollTop = chatMessagesEl.scrollHeight;
    }

    // Handle contact selection
    function selectContact(contactId) {
      if(currentContactId === contactId) return;
      currentContactId = contactId;
      // Update UI
      chatHeaderEl.textContent = contacts.find(c => c.id === contactId)?.name || 'Chat';
      chatInputEl.disabled = false;
      sendButtonEl.disabled = false;
      chatInputEl.value = '';
      chatInputEl.focus();
      renderContacts(searchInputEl.value);
      renderMessages(contactId);
    }

    // Handle sending a message
    function sendMessage() {
      if(!currentContactId) return;
      const text = chatInputEl.value.trim();
      if(!text) return;

      // Save message as sent by user
      const messages = loadMessages(currentContactId);
      const newMessage = {
        text,
        timestamp: Date.now(),
        sentByMe: true
      };
      messages.push(newMessage);
      saveMessages(currentContactId, messages);

      chatInputEl.value = '';
      renderMessages(currentContactId);
      updateContactLastMessage(currentContactId, text);

      // Simulate reply after delay
      simulateReply(currentContactId);
    }

    // Simulate a reply from the contact after 1-3 secs
    function simulateReply(contactId) {
      setTimeout(() => {
        const messages = loadMessages(contactId);
        if(currentContactId !== contactId) return; // if user switched contact, skip reply
        const replies = [
          "Sounds great!",
          "Okay, got it.",
          "Thanks for the update.",
          "I'll get back to you ASAP.",
          "Can you explain more?",
          "Good point!",
          "Let's catch up later.",
          "👍",
          "😊",
          "😂",
        ];
        const replyText = replies[Math.floor(Math.random() * replies.length)];

        messages.push({
          text: replyText,
          timestamp: Date.now(),
          sentByMe: false
        });
        saveMessages(contactId, messages);
        renderMessages(contactId);
        updateContactLastMessage(contactId, replyText);
      }, 1500 + Math.random() * 1500);
    }

    // Event listeners

    // Contact click
    contactsListEl.addEventListener('click', e => {
      const contactEl = e.target.closest('.contact-item');
      if(!contactEl) return;
      const contactId = contactEl.getAttribute('data-contact-id');
      selectContact(contactId);
    });

    // Contact keyboard access (enter or space)
    contactsListEl.addEventListener('keydown', e => {
      if(e.key === 'Enter' || e.key === ' ') {
        const contactEl = e.target.closest('.contact-item');
        if(!contactEl) return;
        e.preventDefault();
        const contactId = contactEl.getAttribute('data-contact-id');
        selectContact(contactId);
      }
    });

    // Send button click
    sendButtonEl.addEventListener('click', () => {
      sendMessage();
    });

    // Enter key in input sends message
    chatInputEl.addEventListener('keydown', e => {
      if(e.key === 'Enter' && !e.shiftKey) {
        e.preventDefault();
        sendMessage();
      }
    });

    // Search contacts
    searchInputEl.addEventListener('input', () => {
      renderContacts(searchInputEl.value);
    });

    // Initial render
    renderContacts();

  })();
</script>
</body>
</html>

