# Wonky UI Design

A Svelte-based showcase of unconventional, quirky, and delightfully "wonky" UI components that challenge traditional design patterns while maintaining functionality and user experience.

## 🚀 What is Wonky UI Design?

Wonky UI Design is a creative exploration of user interface components that break away from conventional design norms. This project demonstrates four unique UI components, each with its own distinctive approach to solving common interface problems:

### Featured Components

- **🔊 Volume Slider** - An unconventional audio control interface
- **🔤 Braille Input** - A tactile input method for accessibility and unique interaction
- **🍔 Drop Burger** - A humorous take on dropdown menus with escalating confirmation dialogs
- **📅 Date Picker** - A creative approach to date selection

## ✨ Features

- **Component Carousel**: Navigate through different wonky components with intuitive prev/next controls
- **Responsive Design**: All components adapt to various screen sizes
- **Modern Stack**: Built with Svelte 5 and SvelteKit for optimal performance
- **Accessible**: Components designed with accessibility in mind
- **Interactive Playground**: Experience each component in isolation

## 🛠️ Tech Stack

- **Framework**: [Svelte 5](https://svelte.dev/) with [SvelteKit](https://svelte.dev/docs/kit/introduction)
- **Build Tool**: [Vite](https://vitejs.dev/)
- **Language**: JavaScript/TypeScript
- **Styling**: CSS with Svelte's scoped styling

## 🚀 Quick Start

### Prerequisites

- Node.js (version 16 or higher)
- npm, yarn, or pnpm

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd wonky-ui-design
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   # or
   pnpm install
   ```

3. **Start development server**
   ```bash
   npm run dev
   # or
   yarn dev
   # or
   pnpm dev
   ```

4. **Open your browser**

   Navigate to [http://localhost:5173](http://localhost:5173) to see the application running.

## 🏗️ Project Structure

```
src/
├── lib/
│   └── Components/          # Wonky UI components
│       ├── BrailleInput.svelte    # Braille input component
│       ├── DatePicker.svelte      # Date picker component
│       ├── DropBurger.svelte      # Burger menu component
│       └── SliderVolume.svelte    # Volume slider component
├── routes/
│   └── +page.svelte        # Main application page with carousel
└── app.html               # HTML template
```

## 🎮 Usage

The application features a carousel interface where you can navigate through each wonky component:

- Click **"next"** or **"prev"** buttons to cycle through components
- Each component demonstrates unique interaction patterns
- Experience unconventional approaches to common UI problems

### Component Details

#### Braille Input
Converts 6-dot Braille patterns to text characters, providing an accessible input method that challenges traditional text entry.

#### Drop Burger
A humorous dropdown menu that escalates confirmation dialogs with each ingredient addition, showcasing progressive disclosure patterns.

#### Volume Slider
An unconventional audio control that reimagines how users interact with volume adjustment.

#### Date Picker
A creative approach to date selection that breaks away from standard calendar interfaces.

## 🔧 Development

### Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build

### Development Workflow

1. Make changes to component files in `src/lib/Components/`
2. The carousel in `src/routes/+page.svelte` automatically includes new components
3. Use `pages` array to add new components to the showcase

## 🤝 Contributing

We welcome contributions! Here's how you can help:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-wonky-component`)
3. Add your wonky component to `src/lib/Components/`
4. Update the `pages` array in `src/routes/+page.svelte`
5. Commit your changes (`git commit -m 'Add amazing wonky component'`)
6. Push to the branch (`git push origin feature/amazing-wonky-component`)
7. Open a Pull Request

### Guidelines for New Components

- **Unconventional**: Challenge traditional UI patterns
- **Functional**: Maintain usability despite the "wonkiness"
- **Accessible**: Consider users with different abilities
- **Well-documented**: Include clear JSDoc comments
- **Responsive**: Work across different screen sizes

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgments

- Built with [Svelte](https://svelte.dev/) and [SvelteKit](https://svelte.dev/docs/kit/introduction)
- Inspired by unconventional design thinking and accessibility needs
- Thanks to the open source community for making this possible

---

**Made with ❤️ and a touch of delightful weirdness**
